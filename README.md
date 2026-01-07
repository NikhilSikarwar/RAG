# AI Policy Assistant - RAG Mini-Project

##  Overview
This project is a Retrieval-Augmented Generation (RAG) system built to answer company policy questions accurately. It uses **GPT-OSS 120B** via **Groq** for high-speed reasoning and **ChromaDB** as a vector store.



##  Tech Stack
- **LLM:** GPT-OSS 120B (Groq)
- **Orchestration:** LangChain (Core & Classic)
- **Vector Store:** ChromaDB
- **Embeddings:** HuggingFace (`all-MiniLM-L6-v2`)

##  Prompt Engineering
The core of this project was an iterative prompt design to ensure grounding:

### Initial Prompt (V1)
- **Structure:** "Answer based on context: {context} Question: {question}"
- **Failure:** The model was too "creative" and used internal knowledge for unanswerable questions.

### Improved Prompt (V2) - Final
- **Strategy:** Added **[STRICT GUIDELINES]**, a specific **refusal phrase**, and **citation requirements**.
- **Result:** Successfully eliminated hallucinations. The model now stays 100% within the provided text.

##  Evaluation Results
I tested the system against 5-8 questions ranging from direct hits to out-of-scope queries.

| Question Type | Status | Answer Clarity |
| :--- | :--- | :--- |
| Answerable (Refunds) | | Precise, identified 15% fee. |
| Logic (Shipping $) |  | Correctly handled $50 threshold logic. |
| Partially Answerable | | Divided Canada (Yes) and Mexico (No) correctly. |
| Unanswerable (CEO) |  | **Correctly Refused** (No Hallucination). |

### What I'm Most Proud Of
I am most proud of the **logic-handling**. Using a 120B model allowed the system to understand *exceptions* (like the software activation rule) rather than just retrieving keywords.

### Future Improvements
1. **Reranking:** I would add a Reranker to improve top-k precision.
2. **Hybrid Search:** Adding Keyword search (BM25) would help with specific terms like country names or fee percentages.
