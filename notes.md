# Embedding models 
The first step of the RAG pipeline is choosing the embedding model. In short, the embedding model produces a fixed dimensional vector which encompasses information about the input. 

Why do we need them? For example, if we have 2 paragraphs of text, we can create embeddings for each paragraph and then using cosine similarity, we can see if the embeddings are closer or farther distance-wise. This will tell us if the paragraphs are talking about the same thing or different topics.

## List of possible embdding models to use
### OpenAI embedding: 'text-embedding-3-large'

| Model                   | ~ Pages per dollar | Performance on MTEB eval | Max input |
|-------------------------|--------------------|--------------------------|-----------|
| text-embedding-3-small  | 62,500             | 62.3%                    | 8191      |
| text-embedding-3-large  | 9,615              | 64.6%                    | 8191      |
| text-embedding-ada-002  | 12,500             | 61.0%                    | 8191      |

#### Example Code for OpenAI Embeddings

```python
from openai import OpenAI
import os

OPENAI_API_KEY = os.environ.get("OPENAI_API_KEY", "")
openai_client = OpenAI(api_key=OPENAI_API_KEY)

def openai_embed(query: str, model="text-embedding-3-large"):
   query = query.replace("\n", " ")
   response = openai_client.embeddings.create(input=[query], model=model)
   embedding = response.data[0].embedding
   return embedding

# Example usage (3072 dimensions)
embeddings = openai_embed("This is a text I want to embed")
```

### Microsoft’s E5 Embeddings

| Model                          | BEIR | # of layers | Embedding dimension | Huggingface                          |
|--------------------------------|------|-------------|---------------------|--------------------------------------|
| multilingual-e5-small          | 46.6 | 12          | 384                 | intfloat/multilingual-e5-small       |
| multilingual-e5-base           | 48.9 | 12          | 768                 | intfloat/multilingual-e5-base        |
| multilingual-e5-large          | 51.4 | 24          | 1024                | intfloat/multilingual-e5-large       |
| multilingual-e5-large-instruct | 52.5 | 24          | 1024                | intfloat/multilingual-e5-large-instruct |

#### Example Code for E5 Embeddings

```python
from sentence_transformers import SentenceTransformer

def e5_embed(query: str, model: str):
    if model not in ['large', 'base', 'small', 'large-instruct']:
        raise ValueError(f'Invalid model name {model}')

    embedder = SentenceTransformer(f'intfloat/multilingual-e5-{model}')
    if model == 'large-instruct':
        task = 'Given a short informative text, retrieve relevant topics'
        query = f'Instruct: {task}\nQuery: {query}'

    embeddings = embedder.encode(sentences=[query], convert_to_tensor=False, normalize_embeddings=True)
    return embeddings

# Example usage (768 dimensions)
embeddings = e5_embed('This is a text I want to embed', model='base')
```

### Nomic-text-embed

This is from Ollama models.

`ollama pull nomic-embed-text`

## Text extraction from PDFs

### PyMuPDF

PyMuPDF requires Python 3.8 or later, install using pip with:

`pip install PyMuPDF`

Usage
Basic usage is as follows:

```python
import pymupdf # imports the pymupdf library
doc = pymupdf.open("example.pdf") # open a document
for page in doc: # iterate the document pages
    text = page.get_text() # get plain text encoded as UTF-8
```