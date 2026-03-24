# Kompass | Local LLM + RAG Chatbot for International Student Onboarding

## Project Overview

This project develops **Kompass**, a conversational AI assistant for international students at Hochschule Emden/Leer. The system uses a **Local LLM + RAG (Retrieval-Augmented Generation)** architecture to answer onboarding questions strictly from official university sources, always citing where the information came from.

The project is based on content from **Moodle pages** (General Information, Semester pages) and **linked PDF documents** maintained by the Coordination Office. The chatbot retrieves relevant content before generating answers, ensuring responses are grounded in verified information rather than hallucinated.

The main objective is to reduce repetitive questions to the Coordination Office while providing students with instant, accurate, and trustworthy answers about university processes and life in Emden.

## Objectives

- understand the information needs of new international students during onboarding
- scrape and prepare content from Moodle pages and PDF documents
- transform documents into embeddings suitable for semantic retrieval
- implement a RAG pipeline that retrieves relevant content before generating answers
- deploy a local LLM that generates responses strictly from retrieved context
- ensure all responses include source citations and "last updated" timestamps
- provide an admin dashboard for the Coordination Office to monitor usage and content freshness
- document methodology, results, and project management artifacts in the repository structure used for the course

## Data Sources

- **Source:** Moodle pages (General Information, Summer/Winter Semester pages), linked PDFs
- **Data Type:** unstructured text, semi-structured web content, PDF documents
- **Unit of Analysis:** document chunks with source metadata
- **Target Output:** natural language answers with citations

The data sources are suitable for this project because they represent the official, verified information that students need during onboarding, maintained by the Coordination Office.

## Data Description

### Content Structure

- content is organized across multiple Moodle pages and linked PDF documents
- each source covers specific topics (IT setup, city registration, campus life, etc.)
- information is updated by the Coordination Office as processes change

### Content Categories

The knowledge base covers several topic areas:

- **University Account & IT Setup** — email activation, campus WiFi, portal access
- **Administrative Processes** — city registration, required documents, semester ticket
- **Campus Life** — Mensa payments, campus card, library, events
- **Academics** — courses, credit points, exam registration
- **Housing** — finding accommodation in Emden
- **Life in Emden** — local tips from previous students (groceries, social spots, etc.)

### Target Behavior

- the chatbot answers questions from retrieved content only
- if no relevant content is found, it responds with "I don't have this information" and redirects to the Coordination Office
- off-topic or general knowledge questions are politely refused

### Update Dimension

- content is scraped daily to capture updates from Moodle
- each response includes a "last updated" timestamp from the source metadata

## Methodology

The methodology follows the **Knowledge Discovery in Databases (KDD)** process presented in the course material.

```text
Databases
    |
    v
Data Selection --> Data Preparation --> Data Transformation --> Data Mining --> Model, Patterns
      ^                   ^                     ^                    |
      |                   |                     |                    v
      +-------------------+---------------------+------ Evaluation, Verification
```

### 1. Problem Understanding

- define the application domain as **student onboarding information retrieval**
- formulate the task as a **question-answering system** grounded in official sources
- specify the project objective: provide instant, accurate answers with citations
- define success criteria in terms of answer accuracy, source grounding, and user experience

### 2. Database

- describe Moodle pages and PDF documents as the central knowledge sources
- identify the available content types and their update frequency
- document assumptions about content structure and availability

### 3. Data Selection

- determine which Moodle pages and PDFs are relevant for the knowledge base
- justify inclusion or exclusion of sources based on relevance and authority
- define the scope of content to be ingested

### 4. Data Preparation

- scrape text content from Moodle pages
- extract text from linked PDF documents
- handle formatting issues, duplicates, and inconsistencies
- prepare clean text with source metadata for transformation

### 5. Data Transformation

- chunk documents into segments suitable for embedding
- generate vector embeddings for semantic search
- store embeddings in a vector database with source metadata
- prepare retrieval pipeline for query-time lookups

### 6. Data Mining

This phase covers the RAG pipeline and LLM response generation.

- **Retrieval** — semantic search to find relevant document chunks for each query
- **Augmentation** — construct prompts with retrieved context
- **Generation** — local LLM generates answers strictly from provided context
- document prompt engineering, model selection, and generation parameters

### 7. Evaluation and Verification

The resulting system is assessed against the project objectives.

- evaluate answer accuracy against known correct answers
- verify source citations match retrieved content
- test fallback behavior for unknown and off-topic questions
- assess response quality and user experience

### 8. Deployment Perspective

- deploy as a public web application accessible without login
- implement responsive chat interface for mobile, tablet, and desktop
- provide admin dashboard for Coordination Office
- document deployment architecture and access patterns

### 9. Monitoring and Maintenance Perspective

- implement daily automated scraping to keep content current
- log unanswered questions to identify knowledge gaps
- track usage metrics (question count, popular topics)
- provide manual refresh trigger for urgent content updates

## Architecture

```text
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Web Client    │────▶│   Backend API   │────▶│   Local LLM     │
│   (Chat UI)     │◀────│                 │◀────│                 │
└─────────────────┘     └────────┬────────┘     └─────────────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │   Vector DB     │
                        │   (RAG Store)   │
                        └────────┬────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │ Content Scraper │
                        │ (Moodle + PDFs) │
                        └─────────────────┘
```

### Key Components

- **Local LLM** — runs locally without external API dependencies
- **Vector Database** — stores document embeddings for semantic search
- **RAG Pipeline** — retrieves relevant content before generating answers
- **Content Scraper** — automatically syncs content from Moodle daily
- **Web Interface** — responsive chat UI accessible on any device
- **Admin Dashboard** — usage metrics and content management for Coordination Office

## Technology Stack

- Python
- FastAPI
- Ollama / llama.cpp
- ChromaDB / FAISS
- sentence-transformers
- BeautifulSoup / Playwright
- React / Next.js

## Repository Structure

This repository follows the documentation-oriented folder structure used in the course.

- `Code/`
  - implementation area for backend, frontend, scraper, and RAG pipeline
- `MLbib/`
  - bibliography files and literature management for the report
- `Manual/`
  - user manual written in LaTeX
- `Poster/`
  - poster source files and generated output
- `Presentations/`
  - presentation material and templates
- `ProjectManagement/`
  - planning documents, checklists, and evaluation criteria
- `report/`
  - main written report structure, figures, and LaTeX content
- `author.xlsx`
  - author and project metadata

## Documentation Entry Points

- Report structure and chapters: `report/`
- Manual source: `Manual/`
- Poster source: `Poster/`
- Presentation material: `Presentations/`
- Literature and citations: `MLbib/`

## Planned Workflow

- document domain knowledge, KDD methodology, and results in `report/`
- maintain literature and citations in `MLbib/`
- develop code artifacts under `Code/`
- prepare supporting deliverables in `Manual/`, `Poster/`, and `Presentations/`
- store planning and evaluation material in `ProjectManagement/`
- review results iteratively in line with the KDD process

## Status

The project topic and methodological direction are now defined as:

**Local LLM + RAG Chatbot for International Student Onboarding using Moodle content and PDF documents as the knowledge base, with source citations and admin monitoring.**

System results and evaluation metrics will be added to this README once the implementation and evaluation phase is completed.
# Kompass
