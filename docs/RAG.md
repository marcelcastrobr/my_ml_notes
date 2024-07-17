# Retrieval Augumented Generation



## Promp Engineering versus RAG versus Fine Tuning 

![image-20231114095854888](./assets/image-20231114095854888.png)



Prompt engineering example:

![image-20231114100356222](./assets/image-20231114100356222.png)



RAG versus Fine tuning

![image-20231114100618413](./assets/image-20231114100618413.png)

Example from OpenAI

![image-20231114101043664](./assets/image-20231114101043664.png)

Re-ranking: Apply across enconder or rule-based.

Classification step: having. the model to classify domain and give extra metadata on the prompt.

Tools: category of questions, e.g.. figures, acccess to SQL databases, etc..

Query expansion: List of question in prompt executed in paralell.

##### How to evaluate?

Picture below is based on [RAGAS -   *Evaluation framework for your Retrieval Augmented Generation (RAG) pipelines*](https://github.com/explodinggradients/ragas). Re. AWS-Bedrock example [here](https://github.com/explodinggradients/ragas/blob/132d5cd10fd9c0856543a4da43fc43c6d7b57ec4/docs/howtos/customisations/aws-bedrock.ipynb) and blog to ry [here](https://explodinggradients.com/evaluating-rag-pipelines-with-ragas-langsmith).

![image-20231114102045866](./assets/image-20231114102045866.png)





## Techniques

### Text-to-SQL

### **Pattern: [Direct Schema Inference, Self-Correction & Optimization](https://github.com/arunpshankar/LLM-Text-to-SQL-Architectures/blob/main/05-Pattern-V/01-self-correct-rank-by-latency-chat.ipynb)**

**Direct schema inference:** ‘*seed prompt*’ that instructs the LLM to construct an SQL query corresponding to a user’s inquiry.The execution of this initial prompt continues iteratively until it meets with success.

```sql
Please craft a SQL query for BigQuery that addresses the following QUESTION provided below. 
Ensure you reference the appropriate BigQuery tables and column names provided in the SCHEMA below. 
When joining tables, employ type coercion to guarantee data type consistency for the join columns. 
Additionally, the output column names should specify units where applicable.\n
QUESTION:
{}\n
SCHEMA:
{}\n
IMPORTANT: 
Use ONLY DATETIME and DO NOT use TIMESTAMP.
--
Ensure your SQL query accurately defines both the start and end of the DATETIME range.
```

**Self-correction**:f ailures are treated as critical learning opportunity for the LLM,  allowing it to scrutinize tracebacks and utilize error messages to  refine and evolve the seed prompt into an improved query iteration.

```sql
prompt = f"""Encountered an error: {msg}. 
To address this, please generate an alternative SQL query response that avoids this specific error. 
Follow the instructions mentioned above to remediate the error. 

Modify the below SQL query to resolve the issue:
{generated_sql_query}

Ensure the revised SQL query aligns precisely with the requirements outlined in the initial question."""
```

**Optimization**:

![image-20231115074047300](./assets/image-20231115074047300.png)



## Dealing with Hallucination

> Reducing hallucination:
>
> a. Prompt Engineering: Your prompt is quite explicit, but you may  want to make it even more stringent. You could add sentences that  explicitly ask the model not to extrapolate from the data. What  temperature are you using?
>
> b. Confidence Scoring: Implement a confidence score mechanism to  assess the relevance of the generated response to the query and the  provided content. If the score is below a certain threshold, default to  “Sorry, I am unable to answer your query.”
>
> c. Post-processing: After the model generates an answer, you could  add another layer of validation to verify the factual accuracy of the  response against the data before sending it to the user.
>
> d. User Feedback Loop: Allow users to flag incorrect answers, which  could be used to fine-tune the model or adjust its confidence  thresholds.
>
> From: [Hallucination in retrieval augmented chatbot (RAG)](https://community.openai.com/t/hallucination-in-retrieval-augmented-chatbot-rag/408275)



## Advanced RAG Techniques:

Figure below presents the common failures of a standard RAG method by [Barnett S. et al.](https://arxiv.org/pdf/2401.05856.pdf). Basically those possible common failures are:

- **Missing content**: cannot answer a question since documents is not available.
- **Missed the Top Ranked Documents:** answer to question was not ranked high enougth thus not appear in result.
- **Not in Context - Consolidation strategy Limitations**: answer did not make into the context for generating the final answer.
- **Not Extracted**: answer present in context but LLM does not present in final answer.
- **Wrong Format:** LLM ignore certain formats 
- **Incorrect Specificity**: answer in LLM response but not specific enougth.
- **Incomplete**: answer not incorrect but miss information.

![image-20240306175319053](./assets/image-20240306175319053.png)

Picture by [Authors](https://arxiv.org/pdf/2401.05856.pdf)

Furthermore, standard RAG methods can only retrieve contiguous chunks from the document corpus, lacking understanding of the overall document context. Therefore the need for advanced RAG methods that allow solution to understand long document context and integrate knowledge from multiple parts of a text, such as an entire book.



## [RAPTOR - Recursive Abstractive Processing For Tree-Organized Retrieval](htt	ps://arxiv.org/html/2401.18059v1)

RAPTOR is an indexing and retrieval system that uses a tree structure to capture both high-level and low-level details about a text. RAPTOR cluster chunks of text, generates text summaries of those clusters and then repeats, generating a tree from the bottom up. This allows it to load into an LLM´s context chunks representing the text at different levels so that it can effectively and efficienltl answer questions at different levels.

![image-20240305214929149](./assets/image-20240305214929149.png)

Picture by Paper´s author

![image-20240305215853619](./assets/image-20240305215853619.png)

Picture by Langchain



The motivation behind RAPTOR is that long texts often presents subtopics and hierarchical structures. Thus the RAPTOR solution builds a recursive tree structure that balances broader topic comprehension with granular details and which allows nodes to be grouped based on semantic similarity not just order in the text.

RAPTOR steps are:

- segment the retrieval corpus into short, contiguous text of length
- Chunks and corresponding SBERT embeddings are used to build the leaf nodes.
- Similar text chunks are grouped using a GMM clustering algorithm. 
- Clustered texts are then summarized and re-embedded into the vector store using gpt-3.5-turbo

The clustering approache uses soft clustering where nodes can belong to multiple clusters without requiring a fixed numbe of clusters. Thus text segments can endup in multiple summaries as it might be relevant to various topics. The clustering algorithm is based on GMM (Gaussian Mixture Models).

RAPTOR steps in querying are:

- Start at the root layer and compute the cosine similarity between the query embedding and the embeddings of all nodes present at the root layer.
- Tree-traversal method selects the top-k most relevant root nodes based on their cosine similarity to the query embedding.
- Text from all selected nodes is concatenated to form the retrieved context

RAPTOR queries uses two strategies: tree traversal and collapsed tree. 

![image-20240305230255337](./assets/image-20240305230255337.png)

Picture by Authors 

Colapsed tree is better as it offers greater flexibility than tree traversal.

Benefits:

- computational efficiency as systems scales lineraly in terms of build time and token expenditure.



Source code: https://github.com/parthsarthi03/raptor

Langchain implementation: https://github.com/langchain-ai/langchain/blob/master/cookbook/RAPTOR.ipynb



### [Graph Neural Network with Large Language Models (Amazon)](https://www.amazon.science/publications/graph-neural-prompting-with-large-language-models)

GNN method has th

![image-20240305230513487](./assets/image-20240305230513487.png)

Picture by Authors

![image-20240305230452152](./assets/image-20240305230452152.png)

Picture by Authors

## References:

- [Architectural Patterns for Text-to-SQL: Leveraging LLMs for Enhanced BigQuery Interactions](https://medium.com/google-cloud/architectural-patterns-for-text-to-sql-leveraging-llms-for-enhanced-bigquery-interactions-59756a749e15)
- [12 RAG Pain Points and Proposed Solutions](https://towardsdatascience.com/12-rag-pain-points-and-proposed-solutions-43709939a28c)
- https://github.com/nerdai/talks/blob/main/2024/mlops/mlops-rag-bootcamp.ipynb
- https://docs.google.com/presentation/d/1mJUiPBdtf58NfuSEQ7pVSEQ2Oqmek7F1i4gBwR6JDss/edit?pli=1#slide=id.g2c566abeaf8_4_18
- https://drive.google.com/file/d/1ku8_5NL2Uv95cger7sPTyODJ8uGRDdZ4/view
- https://www.youtube.com/watch?v=bNqSRNMgwhQ
- https://docs.smith.langchain.com/cookbook/testing-examples/rag_eval#type-1-reference-answer
- Building an Observable arXiv RAG Chatbot with LangChain, Chainlit, and Literal AI - https://towardsdatascience.com/building-an-observable-arxiv-rag-chatbot-with-langchain-chainlit-and-literal-ai-9c345fcd1cd8