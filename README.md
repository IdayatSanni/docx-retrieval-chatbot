# DOCX Retrieval Chatbot

A lightweight document-retrieval chatbot built with Python that allows users to ask questions about the contents of a Word document.

The project demonstrates how a `.docx` document can be transformed into a searchable knowledge base using text preprocessing, text chunking, TF-IDF vectorization, and cosine similarity.

## Overview

The chatbot takes a Word document, extracts its text, divides the content into smaller overlapping passages, and creates a TF-IDF index.

When a user asks a question, the system compares the question against the document passages and retrieves the most relevant content.

### Workflow

```text
Word Document
      ↓
Text Extraction
      ↓
Text Preprocessing
      ↓
Text Chunking
      ↓
TF-IDF Index
      ↓
User Question
      ↓
TF-IDF Query Vector
      ↓
Cosine Similarity
      ↓
Relevant Passages
      ↓
Chatbot Response

## Features

- Extracts text from `.docx` documents
- Cleans and normalizes text
- Splits documents into overlapping text chunks
- Creates a TF-IDF index
- Uses unigrams and bigrams for retrieval
- Calculates cosine similarity between questions and document passages
- Returns the most relevant passages
- Uses a configurable confidence threshold
- Supports custom document-based knowledge bases

## Technology Stack

- Python
- scikit-learn
- python-docx
- TF-IDF
- Cosine Similarity
- Jupyter Notebook

## How It Works

### 1. Document Extraction

The chatbot uses `python-docx` to extract non-empty paragraphs from a Word document.

```python
from docx import Document

doc = Document(path)

paragraphs = []

for p in doc.paragraphs:
    text = (p.text or "").strip()

    if text:
        paragraphs.append(text)
```

### 2. Text Preprocessing

The extracted text is normalized before retrieval.

The preprocessing includes:

- Converting text to lowercase
- Removing extra whitespace
- Removing punctuation

### 3. Text Chunking

The document is divided into smaller passages to make retrieval more manageable.

The current implementation uses:

- Maximum chunk size: 140 words
- Overlap: 30 words

The overlap helps preserve context between adjacent passages.

### 4. TF-IDF Retrieval

The chatbot uses TF-IDF to represent document chunks numerically.

Both single words and two-word combinations are considered:

```python
TfidfVectorizer(
    ngram_range=(1, 2),
    min_df=1
)
```

### 5. Cosine Similarity

When a user submits a question, the question is converted into a TF-IDF vector and compared against the document chunks using cosine similarity.

The highest-scoring passages are returned as the most relevant matches.

## Example Knowledge Base

The chatbot was tested using a custom Q&A document covering Artificial Intelligence, machine learning, and data analytics.

The knowledge base contains 30 questions and answers covering topics such as:

- Artificial Intelligence
- Machine Learning
- Deep Learning
- Natural Language Processing
- Computer Vision
- Data Mining
- Predictive Analytics
- Supervised Learning
- Unsupervised Learning
- Generative AI
- Data Governance

## Example Interaction

### User

```text
What is machine learning?
```

### Chatbot

```text
Machine learning is a subset of AI that enables systems
to learn patterns from data and improve performance
without being explicitly programmed.
```

The chatbot also returns a similarity score for the retrieved result.

For example:

```text
Top match score: 0.46
```

## Confidence Threshold

The chatbot uses a similarity score to determine whether a retrieved passage is relevant enough to return.

The confidence threshold was modified from:

```python
min_conf = 0.16
```

to:

```python
min_conf = 0.30
```

If the best matching passage falls below the threshold, the chatbot responds that it could not find a confident match and asks the user to rephrase the question.

This provides a simple mechanism for reducing responses based on weak document matches.

## Project Structure

```text
docx-retrieval-chatbot/
│
├── notebooks/
│   └── docx_retrieval_chatbot.ipynb
│
├── data/
│   └── README.md
│
├── README.md
├── requirements.txt
└── .gitignore

## What I Learned

This project helped me explore:

- Document processing with Python
- Natural Language Processing
- Text preprocessing
- Text chunking
- Information retrieval
- TF-IDF vectorization
- Cosine similarity
- Similarity-based confidence thresholds
- Building reusable Python classes
- Working with document-based knowledge bases

## Limitations

This project uses traditional information retrieval rather than a generative Large Language Model.

The chatbot retrieves relevant passages from the source document rather than generating a new answer from an LLM.

Because retrieval is based on TF-IDF similarity, queries that use very different wording from the source document may produce weaker matches.

## Future Improvements

Potential improvements include:

- Replace TF-IDF with embedding-based semantic search
- Add a vector database such as Qdrant
- Integrate an LLM for answer generation
- Add source citations to responses
- Build a web-based chat interface
- Support PDF and additional document formats
- Evaluate retrieval performance using a larger test dataset

## Author

**Idayat Sanni**

AI Integration & Governance | Web Development | AI & Machine Learning

[LinkedIn](https://www.linkedin.com/in/idayat-sanni/)