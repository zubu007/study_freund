# Embedding models 
The first step of the RAG pipeline is choosing the embedding model. In short, the embedding model produces a fixed dimensional vector which encompasses information about the input. 

Why do we need them? For example, if we have 2 paragraphs of text, we can create embeddings for each paragraph and then using cosine similarity, we can see if the embeddings are closer or farther distance-wise. This will tell us if the paragraphs are talking about the same thing or different topics.

## List of possible embdding models to use
* OpenAI embedding: 'text-embedding-3-large'
| Model                   | ~ Pages per dollar | Performance on MTEB eval | Max input |
|-------------------------|--------------------|--------------------------|-----------|
| text-embedding-3-small  | 62,500             | 62.3%                    | 8191      |
| text-embedding-3-large  | 9,615              | 64.6%                    | 8191      |
| text-embedding-ada-002  | 12,500             | 61.0%                    | 8191      |
