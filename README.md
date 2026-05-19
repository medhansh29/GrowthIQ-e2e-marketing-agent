# 🚀 GrowthIQ: E2E AI Marketing Agent

An end-to-end AI-powered marketing strategy agent built with **FastAPI**, **LangChain**, and **OpenAI**. 

GrowthIQ acts as an autonomous marketing strategist. It analyzes business context, products, and features to dynamically generate, modify, and synergize high-converting target audiences, strategic growth levers, and step-by-step campaign flows.

## 🛠️ Tech Stack

* **Backend Framework:** FastAPI, Python (Asyncio)
* **AI/LLM Orchestration:** LangChain (`langchain_core`, `langchain_openai`), OpenAI (`gpt-4o`)
* **Data Validation:** Pydantic (Strict schema enforcement for LLM JSON outputs)
* **Database & Auth:** Supabase (PostgreSQL)
* **Environment Management:** `python-dotenv`

## ✨ Core Features

GrowthIQ relies on a multi-agent orchestration architecture to handle complex marketing strategies. 

* 🎯 **Audience Analysis (`audience_analyser.py`):** Automatically generates highly specific audience cohorts (e.g., "Eco-conscious Urban Professionals"). It fetches real business/product context from Supabase to inform the LLM, outputting estimated audience sizes, cohort scores, and JSON-based segmentation rules.
* 📈 **Growth Lever Generation (`growth_levers.py`):** Proposes strategic initiatives tailored to user prompts. Outputs include behavioral signals, implementation channels, estimated metric lift, and projected ROI.
* orchestrator **Campaign Flow Orchestration (`campaign_generator.py`):** Synergizes generated audiences and growth levers to create complete, step-by-step marketing campaigns. Includes estimated reach, expected CTR, and expected conversion rates.
* 🧠 **Stateful Session Memory:** The API is designed to manage "UI Session Memory," allowing users to generate, modify, and delete artifacts in-memory before committing the final approved strategy to the Supabase database via a `/finalize` endpoint.

## 🏗️ Architecture & Data Flow

1.  **Context Retrieval:** The system retrieves current `business_context_store`, `product_store`, and `feature_store` data from Supabase to ground the AI's generation.
2.  **LLM Processing:** User prompts are combined with this context using LangChain `ChatPromptTemplate`s.
3.  **Structured Output:** LangChain's `PydanticOutputParser` forces the `gpt-4o` model to return strictly typed JSON objects representing complex marketing data.
4.  **Database Persistence:** Once a user finalizes a session, data is upserted into respective Supabase tables (`audience_store`, `growth_levers_store`, `campaigns`).

## 🚦 API Endpoints Overview

The API provides CRUD-style operations over in-memory state, plus database finalization.

* `/audiences/*` (`/generate`, `/modify`, `/delete`, `/finalize`)
* `/growth-levers/*` (`/generate`, `/modify`, `/delete`, `/finalize`)
* `/campaign-flows/*` (`/generate`, `/modify`, `/delete`, `/finalize`)

## 🚀 Getting Started

### Prerequisites
* Python 3.9+
* An OpenAI API Key
* A Supabase Project

### Installation

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/medhansh29/GrowthIQ-e2e-marketing-agent.git](https://github.com/medhansh29/GrowthIQ-e2e-marketing-agent.git)
   cd GrowthIQ-e2e-marketing-agent
