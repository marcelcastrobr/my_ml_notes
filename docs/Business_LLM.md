# LLM: Business Point of View:



# Business General

The amount of investiment in generative AI lately has skyrocket.  It jumpt from 2.85 billion US dollars in 2022 to 25.23 billion US dollars in 2023. (ref. [IEEE Spectrum][ref1]).

This has also been reflected on the race on the foundation models lately, that is clearly seen by number of foundation models been released by big industry players like Amazon, Google, Meta, Microsoft and OpenAI for example.

Generative AI is impacting every organization nowadays and an important aspect is how those organization can access the ROI (return of investiment) for generative AI. As described by [Gartner][ref2], generative AI usecases can be divided in the following mix when considering **value** versus **risk**:

**Quick wins**:  task specific usecases with productivity assistants such as [Amazon Q for Developer](https://aws.amazon.com/q/developer/) and Microsoft 365 Copilot. Integrating these capabilities into other business process can help you maintain a competitive edge. Examples are: assistants/copilots, marketing generation and code assistants.

**Differentiating use cases**: industry specific or custom application that leverage your enterprise data in new ways extending your current process. Application such as Retrieval Augumented Generation (**RAG**) enables you to leaverage your enterprise data through for example the use of [Amazon Q for Business](https://aws.amazon.com/q/business/) or [Amazon Bedrock](https://aws.amazon.com/bedrock/). This might lead to potential benefits such as revenue generation. Additional examples are: custom support apps, sales apps, and enterprise document search and summarization.

**Transformational initiatives**: has the potential to turn business and model upside down. Those transformative usecases comes with complexity, risk and cost and high potential for technical depth. Examples are the creation of fine tuning foundation models or even custom pre-trained foundation models such as [BoombergGPT](https://arxiv.org/abs/2303.17564) - a foundation model specialized in financial domain.



<img src="./assets/image-20240607092240764.png" alt="image-20240607092240764" style="zoom:50%;" />



To better understand the cost of generative AI usecases, we describe in the section below the main elements to consider in order to calculate the cost of generative AI applications.

### Cost of Generative AI

Figure below summarize some of the cost related to generative AI, which are composed by:

- **Application Implementation**:
  - **Custom Application Build**: Costs associated with building or modifying the custom application tailored for generative AI.
- **Model Cost**:
  - **Foundation Models**: Costs related to using base or customized foundational models for AI.
- **Infrastructure Cost**:
  - **Cloud Infrastructure**: Expenses related to cloud infrastructure required to support AI operations (either through an API or by deploying those models on computing instances).
- **Data Cost**:
  - **Enterprise Data**: Costs for acquiring and managing enterprise-specific data.
  - **Data Science & Engineering**: Costs for data science and engineering efforts.
  - **Data Governance & Management**: Expenses for managing and governing data.
  - **Public/Vendor Data**: Costs associated with obtaining data from public sources or vendors.
- **User Cost**:
  - **User License**: Costs for licensing users.(e.g. code assistant)
  - **Enablement/Training**: Expenses for training and enabling users to effectively use the AI system.
- **Consumption / Inference Cost**:
  - **Context Size: prompt+answer**: Costs depending on the size of the prompt and the answer generated.
  - **Number of Interactions**: Costs based on the number of interactions.
  - **$ per token / computing instance**: Costs calculated per token or per computing instance used.



This breakdown helps in understanding the multifaceted nature of expenses involved in deploying and maintaining generative AI solutions.

![image-20240607100652721](./assets/image-20240607100652721.png)

### KPIs examples for Generative AI Applications

Implementing and closely monitoring Key Performance Indicators (**KPIs**) is crucial to ensure that the costs associated with generative AI projects are managed effectively and remain within budgetary constraints.

Example of KPIs per usecase mix that might be relevant to keep track on are:

- **Quick wins**
  - number of stories completed, commits, changes per week
  - deployment frequency, pull request interation time
  - lines of code per developer, dev retention
  - time to upskills associates/junior developers
- **Differentiating use cases**
  - time saved to perform tasks (e.g. answer customer support question, create document/process/marketing)
  - employee retention
  - portion of time spent on customer / doing knoledge tasks
  - Time to create content / analyze data / derive insights
  - rework time (i.e. output quality)
  - content output throughput (amount of task per resource)
  - call sastisfaction scores
  - Time to expert skills levels
  - Amound of escalations
  - incremental revenue on upsell/cross sell.
  - customer retention / customer satisfaction
  - Content quality / error rates
- **Transformational initiatives**
  - market share
  - generative AI product revenue.
  - amount of market created
  - time saved to access risk and complexity of contracts/insurance documents
  - Claim cost/processing improvement
  - Brand improvement
  - reduce time to market (e.g. new drug discovery)
  - reduce error rates (e.g. in medicine, law and finance)
  - increase on opportunity and risk prediction



### **References**:

- [ref1]: https://spectrum.ieee.org/ai-index-202415 "Graphs That Explain the State of AI in 2024  - The AI Index tracks the generative AI boom, model costs, and responsible AI use by IEEE Spectrum"

- [ref2]: https://www.gartner.com/en/articles/take-this-view-to-assess-roi-for-generative-ai, "Take This View to Assess ROI for Generative AIby Gartner"

- [ref3]: How to Calculate Business Value and Cost for Generative AI Use Cases by Gartner



# ISV Specific



![image-20240314105552624](./assets/image-20240314105552624.png)

Picture from [EMEA ISV 2024 - Data & GenAI Business Acceleration (Guest Series: Eddie meets Oren)](https://broadcast.amazon.com/videos/1050546?ref=watch_later&src=watch-later)



# AWS Application Examples



### Glue - Generative Data Integration

**Broadcast**: [Generative Data Integration (AWS Glue](https://broadcast.amazon.com/videos/1066838?ref=personal)) 

**What it is**: Glue Data integration as part of Amazon Q. Give an idea of challenges the Glue team had from proof-of-concept to productionizing Generative AI. Thus highly relevant in connection to our **[2024 AGS Tech Goal / G1: Innovation Through GenAI](https://w.amazon.com/bin/view/AGSTECH/Goals2024/GenAI)**.

**Shortcuts**: AWS Glue Journey (0:17:37), Challenges (0:52:00)

**TL;DW:** 

- Need for high quality data integration dataset.
- RAG challenges: Kendra versus OpenSearch
- Production consideration: guardrails (security and prompt injection) and PII detection
- hack != Product -> this might reflect our challenge to help customer on productioning Generative AI in 2024.
- Domain knowledge: *otherwise LLMs and halucination go hand in hand*.
- custom metrics (?): enable product improvement without customer interaction data.



AWS Flock (guardrail): https://w.amazon.com/bin/view/AWS/Flock/ 



# Generative AI Failures on News:

**Driver uses ChatGPT hack to get dealer to agree to sell new car for $1 in ‘legally binding deal’ in blow for AI rollout** - https://www.thesun.co.uk/motors/25091054/driver-uses-ai-loophole-buy-new-car-1/



![image-20240403103226298](./assets/image-20240403103226298.png)

Source: https://abovethelaw.com/2024/01/keep-your-firm-far-away-from-whatever-ai-chevy-was-using/



# Competition

Game: https://gandalf.lakera.ai/

