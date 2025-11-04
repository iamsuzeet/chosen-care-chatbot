# 🤖 AI Chatbot — n8n + Crawl4AI + Whisper + Kokoro + PostgreSQL

A complete **AI Chatbot workflow automation stack** powered by Docker Compose. 

This setup combines workflow automation, web crawling, transcription, and text-to-speech into one cohesive environment.

---

## 🧩 Overview

| Service | Description | Port |
|----------|--------------|------|
| **n8n** | Workflow automation platform | `5678` |
| **PostgreSQL** | Persistent database backend for n8n | `5432` |
| **Crawl4AI** | Intelligent AI web crawling and extraction API | `11235` |
| **Kokoro (FastAPI)** | Text-to-speech (TTS) API service | `8880` |
| **Whisper ASR Webservice** | Speech-to-text (STT) service powered by OpenAI Whisper | `9000` |

All containers communicate via the shared internal `backend` network.

---

## ⚙️ Requirements

Before starting, ensure you have:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/) 
- A valid `.env` file with configuration values (see below)

---

## 🧾 Environment Variables

Replace your environment variable in `.env` file in the project root:

```bash
# General
DOMAIN=your_domain_name
SUBDOMAIN=your_subdomain
GENERIC_TIMEZONE=Europe/London

# Database
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres

# Data paths
DATA_FOLDER=/path/to/data
```

## 💾 Persistent Volumes

| Volume          | Purpose                                 | External |
| --------------- | --------------------------------------- | -------- |
| `n8n_data`      | Stores n8n workflows and configurations | ✅        |
| `n8n_db`        | Stores PostgreSQL data files            | ✅        |
| `cache-whisper` | Caches Whisper ASR model files          | ✅        |

To create the volumes manually (if not yet created):

```bash
docker volume create n8n_data
docker volume create n8n_db
docker volume create cache-whisper
```

## 🚀 Usage

### 1️⃣ Start the Stack

### Local Development

```bash
docker compose up -f docker-compose.yaml -f docker-compose.local.yaml -d
```

### Production

```bash
docker compose up -d
```

### 2️⃣ Access Services

| Service             | URL                                              |
| ------------------- | ------------------------------------------------ |
| **n8n UI**          | [http://localhost:5678](http://localhost:5678)              |
| **Crawl4AI API**    | [http://localhost:11235](http://localhost:11235) |
| **Kokoro API**      | [http://localhost:8880](http://localhost:8880)   |
| **Whisper ASR API** | [http://localhost:9000](http://localhost:9000)   |


#### 🧾 Create and Upload your workflow in n8n UI

Upload the `chat-bot.json` file from the directory to the n8n.

![alt text](image-2.png)

### 3️⃣ Test the bot

1. Get the webhook url from the n8n workflow UI
    ![alt text](image-1.png)

2. replace the webhook url in `index.html` under `n8nChatUrl`.
   
   ![alt text](image.png)

Open `index.html` and chat with the bot.



