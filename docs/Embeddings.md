# The World of Embedding in Natural Language Processing



**Definition:**

Embeddings are continuous **vector** representation of words or tokens capturing semantic representation in a high dimensional space.

Since machines does not understand words, we need to first convert them to number in a process called tokenization. 



**Word similarity** is important in semantic tasks. For example to know how similar  two words are can help in identifying the similarity of phrases or sentences where those words are used.

Vector semantics is the way to represent word meaning in NLP (Natural Language Processing) [~Ref1].  The idea of vector semantics is to represent a word as a point in a multidimentional space that is derived from a distribution of word neighbors. Thus **vectors** for representing words are called **embeddings**.

**Word2vec** is a common example of dense vectors. Figure below shows a two-dimensional PCA projection of embeddings for some words using word2vec model which visualize how embeddings learned the semantic meaning. of the words (e.g. countries are grouped together in the vector space.)

![img](./assets/cell-10-output-1.png)

Picture: Image by Author ([~Ref2])



**Measuring Similarity** between two words (v and w) is normally done using cosine function - based on teh dot product operator from linear algebra (a.k.a. inner product) [~Ref1].
$$
dot-product(v,w) = v.w\sum_{i=1}^{N} v_i w_i
$$




## References:

[~Ref1]: [Dan Jurafsky’s book on language models](https://web.stanford.edu/~jurafsky/slp3/6.pdf)

[ ~Ref2] [Notes on Natural Langage Processing with Deep Learning](https://marcelcastrobr.github.io/posts/2022-01-04-nlpdeeplearning.html)

[ ~Ref3]

[ ~Ref4]

[ ~Ref5]