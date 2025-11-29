# 🤖 AI Gmail Support System – Muazzam Ali

This repository contains a fully automated **AI-powered customer support system** built using **n8n**, **OpenAI**, **Google Gemini**, **Google Sheets**, **Slack**, **Google Drive**, and **Pinecone RAG**.

The system automatically:
- Reads incoming emails from Gmail  
- Classifies ticket type using AI  
- Routes to the correct AI Support Agent  
- Searches internal docs using Pinecone RAG  
- Sends auto-generated Gmail replies  
- Logs all support interactions to Google Sheets  
- Escalates urgent issues to Slack  
- Updates documentation automatically from Google Drive  

---

## 🚀 Features

### 🔹 1. Email Classification  
AI automatically categorizes emails into:
- Technical Support  
- Billing  
- General Inquiry  
- Urgent Escalation  

### 🔹 2. Specialized AI Agents  
Each support type is handled by a different agent:
- Technical Support Agent  
- Billing Support Agent  
- General Support Agent  
- Urgent Escalation Agent  

All agents use:
- **Google Gemini for reasoning**
- **OpenAI embeddings**
- **Pinecone Vector Store** for knowledge retrieval

---

## 🧠 RAG (Retrieval-Augmented Generation)

The workflow dynamically loads documents from Google Drive:
- Extracts text  
- Splits into chunks  
- Generates embeddings  
- Stores in Pinecone  

Agents query the vector store to answer customer questions using **your real documentation**.

---

## 📊 Google Sheets Dashboard

Every ticket is logged with:
- Email  
- Category  
- AI response  
- Timestamp  
- Escalation state  

Perfect for tracking and reporting.

---

## ⚠️ Slack Human Escalation

If the system identifies an **urgent** message:
- It pushes a notification to Slack  
- Includes full context and email body  

---

## ✉️ Gmail Autoresponder

AI writes and sends a professional reply using Gmail API.

---

## 🧩 Tech Stack

| Category | Technology |
|---------|------------|
| Automation | n8n |
| AI Models | Google Gemini, OpenAI |
| Vector DB | Pinecone |
| Embeddings | OpenAI |
| Storage | Google Drive |
| Logging | Google Sheets |
| Escalation | Slack |
| Email Intake | Gmail Trigger |

---

## 📂 Files Included
- `workflow.json` – full n8n automation workflow  
- `README.md` – documentation (this file)

---


