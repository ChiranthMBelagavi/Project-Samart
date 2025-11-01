# Project Samarth: Intelligent Q&A Prototype

A functional prototype of an intelligent Q&A system built for the Project Samarth challenge. This system is designed to answer complex, natural language questions by synthesizing siloed data from the Ministry of Agriculture and the IMD (India Meteorological Department).

---

## The Problem

Government portals like `data.gov.in` host thousands of valuable datasets. However, this data exists in varied formats and inconsistent structures across different ministries. This makes it extremely difficult for policymakers and researchers to derive the cross-domain insights needed for effective decision-making (e.g., "How do rainfall patterns in a region affect its crop production?").

## The Solution: A "Vertical Slice" Prototype

This repository contains a functional, end-to-end "vertical slice" of a robust solution. It demonstrates how to solve the core problem of data integration and querying.

This prototype consists of two key parts:
1.  **`demo.html`**: A standalone frontend simulation used to record the live demo.
2.  **`main.py`**: The complete, functional Python code for the backend, used to explain the system's architecture.

---

## System Architecture: The "Intelligent Pipeline"

My key design choice was to **not** feed raw data to an LLM. This avoids hallucinations and ensures 100% data accuracy. Instead, I designed an "Intelligent Pipeline" that separates logic from data.

****

1.  **Frontend (`demo.html`)**: A simple, clean chat interface where the user asks a question in natural language.

2.  **Intelligent Q&A Layer (LLM Router)**: As shown in `main.py` (in the `get_query_plan` function), the user's question is sent to an LLM. The LLM's **only job** is to act as a **Query Router**. It parses the unstructured question into a structured JSON "query plan".

3.  **Data Synthesis Layer (Pandas)**: This JSON plan is then passed to the `execute_plan` function. This function uses **Pandas** to programmatically query, filter, and join the *actual* (simulated) dataframes. It performs all calculations and analysis.

4.  **Synthesized Response**: The function builds a final Markdown report *only* from the real data, which is then sent back to the user.

---

## Core Features

* **Cross-Domain Synthesis**: Answers complex questions that require data from both the (simulated) Agriculture and IMD datasets.
* **Accuracy & Traceability**: The LLM *never* sees the data or makes up an answer. The answer is 100% generated from the Pandas dataframes, and each data point in the final report explicitly **cites its source**.
* **Scalable Design**: This "Router -> Synthesis" pattern is highly scalable. New data sources (e.g., "Fertilizer Data") can be added by simply creating a new Pandas function and updating the LLM's prompt.

---

## How to View This Prototype

This repository contains two files to demonstrate the complete project.

### 1. The Live Demo (Frontend)

This file simulates the full user experience.
* **File**: `demo.html`
* **How to Run**: Just double-click this file to open it in any web browser.
* **Function**: This is a standalone simulation. It does **not** require Python or an API key. It accepts the sample question, shows a "Thinking..." message, and then displays a perfect, "ready-made" answer to demonstrate the final output.

### 2. The System Architecture (Backend)

This file contains the complete, working code for the backend.
* **File**: `main.py`
* **How to Use**: Open this file in any code editor (like VS Code).
* **Function**: This file is used to **show and explain** the core architectural components (the FastAPI server, the `get_query_plan` (LLM) function, and the `execute_plan` (Pandas) function) during the video.
