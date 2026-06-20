# 🍔 FoodHub CX Support Chatbot

An AI-powered customer support chatbot for a food delivery platform, built with a fully LLM-driven conversation flow. Customers can authenticate and query their order details — status, delivery time, payment, and more — through natural language.

---

## 🚀 Live Demo

[FoodHub CX Chatbot on Hugging Face Spaces](https://rajse-food-delivery-chatbot.hf.space/)


---

## 📌 Project Overview

**Business Problem:**
Food delivery platforms handle large volumes of repetitive customer queries — order status, delivery time, payment confirmation — which are costly and slow to resolve manually.

**Solution:**
An LLM-powered chatbot that connects directly to the order database and handles customer queries in real time through natural, conversational interactions.

---

## 🏗️ Architecture

```
Customer → Streamlit UI → Authentication → LLM (LLaMA 3.1 via HuggingFace)
                                                      ↑
                                          Order data injected into
                                          system prompt from SQLite DB
```

**Conversation Flow:**
1. Customer enters their ID → verified against the order database
2. All their order data is loaded and injected into the LLM system prompt
3. Every message goes directly to the LLM — no keyword routing, no rule-based logic
4. LLM responds naturally using only the customer's own data
5. Full conversation history is maintained across turns

---

## 🧠 Key Features

- **Fully LLM-driven** — LLaMA 3.1-8B-Instruct handles intent, response, and edge cases
- **Session-based authentication** — customers verified by customer ID before any data is shared
- **Data guardrails** — LLM only sees the authenticated customer's own orders
- **Multi-turn memory** — full conversation history passed on every turn
- **Natural language understanding** — handles vague queries, follow-ups, and edge cases
- **Session timeout** — auto-resets after 5 minutes of inactivity

---

## 🗂️ Project Structure

```
├── app.py                          # Streamlit app (fully LLM-driven)
├── requirements.txt                # Python dependencies
├── Dockerfile                      # Docker config for HF Spaces
├── README.md                       
├── customer_orders.db              # SQLite order database
└── food_delivery_CX_query_flow.ipynb  # Development notebook
```

---

## 📓 Notebook Structure

The notebook documents the full development journey:

| Section | Description |
|---|---|
| Problem Statement | Business context and objectives |
| Data Loading | SQLite database connection and loading |
| Data Cleaning | Time column parsing and null handling |
| Data Exploration | Order status, payment status distributions |
| Helper Functions | Pandas-based order lookup functions |
| LLM Setup | HuggingFace InferenceClient configuration |
| Fully LLM-Driven Chatbot | `chat_with_llm()` implementation |
| Local Testing | `run_local_test()` simulating full conversations |
| App Deployment | Streamlit app setup and HF Spaces upload |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| LLM | LLaMA 3.1-8B-Instruct (via Novita provider) |
| LLM API | HuggingFace Inference API |
| Database | SQLite |
| Deployment | Hugging Face Spaces (Docker) |
| Language | Python 3.11 |

---

## ⚙️ Setup and Run Locally

**1. Clone the repo**
```bash
git clone https://github.com/your-username/food-delivery-chatbot.git
cd food-delivery-chatbot
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Set your HuggingFace token**
```bash
export HUGGINGFACEHUB_API_TOKEN=your_token_here
```

**4. Run the app**
```bash
streamlit run app.py
```

---

## 🔐 Environment Variables

| Variable | Description |
|---|---|
| `HUGGINGFACEHUB_API_TOKEN` | Your HuggingFace API token — set as a secret in HF Spaces |

---

## 📦 Dataset

The dataset is sourced from FoodHub's order management database and contains:

| Column | Description |
|---|---|
| `order_id` | Unique order identifier |
| `cust_id` | Customer identifier |
| `order_time` | Timestamp when order was placed |
| `order_status` | Current order status |
| `payment_status` | Payment confirmation |
| `item_in_order` | Items ordered |
| `preparing_eta` | Estimated preparation time |
| `prepared_time` | Actual preparation time |
| `delivery_eta` | Estimated delivery time |
| `delivery_time` | Actual delivery time |

---
