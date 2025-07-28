# Building-a-RAG-system
Retrieval-Augmented Generation (RAG) System for Financial Reports  

Project Overview  

This project implements a Retrieval-Augmented Generation (RAG) system designed to answer natural language questions from financial reports, specifically Meta's Q1 2024 Financial Report. 

Approach  

To build an effective RAG system, we followed a two-stage approach:

1. Basic RAG Pipeline  
2. Structured Data Integration


Step 1: Basic RAG (Text-based QA)
PDF Text Extraction: Extracted raw textual content from Meta’s Q1 2024 financial report using PyMuPDF.


Chunking: Applied overlapping text chunking using LangChain for better context segmentation.


Embeddings: Generated vector representations using the all-MiniLM-L6-v2 model from sentence-transformers.


Vector Store: Stored the chunk embeddings in FAISS (Facebook AI Similarity Search).


Retrieval: Retrieved the top-3 most relevant text chunks using L2 (Euclidean) distance, which computes straight-line distances between vectors in the embedding space.


Answer Generation: Used a lightweight open-source LLM (Qwen/Qwen3-0.6B) to generate answers grounded in the retrieved text chunks.



Sample Queries:
“What was Meta’s revenue in Q1 2024?”


“What were the key financial highlights for Meta in Q1 2024?”



Step 2: Structured Data Integration (Hybrid RAG)
Table Extraction: Parsed structured tables from the PDF using pdfplumber to extract key numerical and tabular data.


Hybrid Retrieval: Combined vector-based semantic retrieval (from Step 1) with keyword-based or SQL-like lookup for structured data, enabling both unstructured and structured data querying.


Prompt Construction: Dynamically constructed LLM prompts containing both:


Retrieved text context


Extracted structured data (e.g., financial figures, table summaries)


Sample Queries:
“What was Meta’s net income in Q1 2024 compared to Q1 2023?”


“Summarize Meta’s operating expenses in Q1 2024.”
Key Results & Observations
The overall output quality was poor across both steps
 The hybrid RAG pipeline with structured data integration did not significantly improve accuracy — in many cases, the model still produced useless or generic outputs.
This was expected, as it was my first time working with RAG pipelines and vector databases, and the entire implementation was driven by a learning-first mindset rather than production-level results.
Despite the poor performance, the project helped me understand the basic workflow of retrieval, embedding, and generation, and taught me what doesn't work — which is equally valuable at this stage.

