# Video RAG System — YouTube Question Answering over Long Context

This project implements a Retrieval-Augmented Generation (RAG) pipeline that allows users to ask questions about a YouTube video and receive grounded answers based on the video transcript.

Unlike simple summarizers, the system retrieves relevant context from the video before generating a response, reducing hallucination and improving factual accuracy.

---

## What Problem This Solves

Large language models are powerful but unreliable when they lack external context.  
Videos contain dense information, but they are difficult to query directly.

The real challenge is not calling an LLM — it is retrieving the *right pieces of information* under token limits.

This project builds a system that:
- converts a video into searchable knowledge
- retrieves relevant transcript segments
- answers user questions grounded in the video

---

## System Pipeline

YouTube Video
→ Transcript Extraction
→ Text Chunking
→ Embedding Generation
→ Vector Index (FAISS)
→ Similarity Retrieval
→ Context Selection
→ LLM Answer

---

## Key Components

### Transcript Ingestion
Uses `youtube-transcript-api` to extract subtitles and convert the video into text.

### Chunking
The transcript is split into smaller segments so retrieval can target relevant information rather than the entire video.

### Embeddings
Each chunk is converted into vector embeddings using an embedding model.  
This allows semantic search rather than keyword matching.

### Vector Retrieval
FAISS is used to store and retrieve the most relevant transcript chunks for a user question.

### Answer Generation
The retrieved chunks are inserted into a prompt and sent to the LLM, ensuring the response is grounded in the video content.

---

## Design Decisions

- Smaller chunk sizes improved retrieval precision but increased query time
- Retrieval quality affected answer accuracy more than model choice
- Grounding responses d

