## 🩺 Medical RAG Assistant

A full end-to-end Retrieval-Augmented Generation pipeline using Kaggle, LangChain, FAISS, and Gemini.

This project builds a Medical Assistant Chatbot using:

Medical Transcription Dataset (mtsamples.csv from Kaggle)

Google Generative AI Embeddings (text-embedding-004)

FAISS Vector Store

Gemini 2.5 Flash / ChatGoogleGenerativeAI

Gradio Chat UI

It embeds ~800 medical transcriptions, builds a vector index with batching & rate-limit protection, and serves a full RAG chatbot.

## Features

✔️ Automated text-splitting and embedding
✔️ Batch-based FAISS index creation with progress bars
✔️ Full RAG chain (Retriever → Prompt → LLM)
✔️ Gradio chat interface with examples
✔️ Index saving + reload test script
✔️ Kaggle-ready, GPU-enabled notebook environment

## 1. Installation
pip install -q langchain langchain-google-genai langchain-community faiss-cpu sentence-transformers gradio python-dotenv


Kaggle will auto-install some packages.
If dependency warnings appear, they do not break this project.

 ## 2. Setup API Key (Kaggle)

Go to:

Kaggle → Settings → Secrets

Create a secret:

Name: GOOGLE_API_KEY
Value: your-key-here

## 3. Dataset

This project uses:

Dataset: Medical Transcriptions (mtsamples)

Kaggle path:

/kaggle/input/medicaltranscriptions/mtsamples.csv

## Dataset Overview — Medical Transcriptions (MTSamples)

This project uses the Medical Transcriptions (MTSamples) dataset available on Kaggle.
It contains:

~5,000 real medical dictations from physicians

Covering 40+ specialties, including:

Cardiology

Neurology

Orthopedics

Dermatology

Gastroenterology

Psychiatry

Radiology

General Surgery

Each sample includes:

description – type of procedure / case

medical_specialty – specialty category

transcription – detailed medical note

Why This Dataset Works Well for RAG

It contains long, detailed clinical narratives, ideal for chunk-based retrieval.

Each transcription uniquely reflects:

Symptoms

Medical histories

Diagnoses

Surgeries

Treatments

It allows the model to answer evidence-based medical questions, unlike synthetic summaries.

What the Dataset Does Not Contain

No patient identifiers (HIPAA stripped)

No structured diagnosis labels

No images, labs, reports — only text

This makes it perfect for:

Medical education projects

Clinical summarization experiments

RAG-based Q/A systems

## Building the FAISS Vector Index

The notebook:

Reads 800 samples (for faster demo)

Splits into ~2,000 chunks

Embeds in batches of 20

Sleeps 2 seconds per batch to avoid rate limits

Saves index to /kaggle/working/faiss_index

Code already optimized for Kaggle: multi-batch, progress bars, safety checks.

## Querying the Index (RAG)

We use:

FAISS Retriever (k=3)

PromptTemplate with clinical guardrails

Gemini 2.5 Flash for response generation

Model only responds based on dataset evidence, and returns lookup-based medical answers.

 ## Gradio Medical Chatbot

The notebook launches:

Title: Medical RAG Assistant

Mode: ChatInterface

Example medical questions

Clean UI with no hallucinations allowed

All answers come from retrieval hits within the dataset.

## Project Structure (Kaggle)
/kaggle/input/medicaltranscriptions/mtsamples.csv   # dataset
/kaggle/working/faiss_index/                       # generated index
/kaggle/working/app.py                             # chatbot script

## Sample Questions You Can Ask

"What are symptoms of allergic rhinitis?"

"Describe the procedure for knee arthroscopy."

"What findings suggest chronic back pain?"

"Explain carpal tunnel release surgery."

All answers are dataset-grounded, contextual, and 100% traceable.

⚠️ Medical Safety Note

This RAG system is only for:

Research

Learning

Demonstration

It does not replace professional clinical judgment.

The model can only answer based on dataset text and should not be used for real medical decisions.
