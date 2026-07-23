# 📰 NewsLens AI — Intelligent News Summarization & Sentiment Analysis System

> Development of an Intelligent News Summarization and Sentiment Analysis System using Natural Language Processing (NLP) and Large Language Models (LLMs)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Folder Structure](#-folder-structure)
- [Installation & Setup](#-installation--setup)
- [Running the Application](#-running-the-application)
- [API Documentation](#-api-documentation)
- [Sample Test Data](#-sample-test-data)
- [Modules Description](#-modules-description)
- [Future Improvements](#-future-improvements)
- [License](#-license)

---

## 🎯 Overview

**NewsLens AI** is a full-stack web application that empowers users to analyze news articles using state-of-the-art Natural Language Processing (NLP) and Large Language Models (LLMs). Users- NLP Preprocessing (tokenization, lemmatization, stopword removal)
- AI-powered summarization using local Hugging Face model (`facebook/bart-large-cnn`)
- Sentiment analysis with confidence scores
- Keyword extraction (top 10)
- Named Entity Recognition
- Question answering grounded in the article using local Hugging Face model (`distilbert-base-cased-distilled-squad`)rms
- **Named Entity Recognition (NER)** identifying people, organizations, locations, and more
- **Interactive Q&A** grounded in the article's content

The system addresses the growing challenge of information overload in digital media by providing a comprehensive, one-click analysis of news content. It combines traditional NLP techniques (tokenization, lemmatization, stopword removal) with modern LLM capabilities to deliver accurate, insightful, and actionable results through an intuitive, responsive web interface.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 📝 **Article Input** | Paste any news article for instant analysis |
| 🔧 **NLP Preprocessing** | Tokenization, lemmatization, and stopword removal pipeline |
| 🤖 **AI-Powered Summarization** | Concise summaries generated using Google Gemini (`gemini-2.0-flash`) |
| 📊 **Sentiment Analysis** | Positive/Negative/Neutral classification with confidence scores (VADER) |
| 🔑 **Keyword Extraction** | Top 10 keywords extracted using YAKE algorithm |
| 🏷️ **Named Entity Recognition** | Identifies people, organizations, locations, dates, and more (spaCy) |
| ❓ **Question Answering** | Ask questions grounded in the article content, answered by Gemini |
| 📈 **Reading Statistics** | Word count, character count, sentence count, and estimated reading time |
| 🌙 **Dark Mode** | Toggle between light and dark themes for comfortable reading |
| 📱 **Responsive Design** | Optimized for desktop, tablet, and mobile viewports |
| 📋 **Copy Summary** | One-click copy of the generated summary to clipboard |
| 📰 **Sample Article** | Pre-loaded sample article for quick demo and testing |
| 🗑️ **Clear Article** | Quickly clear the input and all analysis results |

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | React + Vite | Single-page application with hot module replacement |
| **Frontend** | HTML, CSS, JavaScript | Structure, styling, and interactivity |
| **Backend** | Python 3.9+ | Server-side logic and NLP processing |
| **Backend** | Flask | Lightweight REST API framework |
| **NLP** | NLTK | Tokenization, lemmatization, stopword removal |
| **NLP** | spaCy (`en_core_web_sm`) | Named Entity Recognition (NER) |
| **NLP** | YAKE | Unsupervised keyword extraction |
| **NLP** | VADER Sentiment | Sentiment analysis with compound scores |
| **AI** | Hugging Face (`transformers`, `torch`), BART, DistilBERT |
| **Other** | python-dotenv | Environment variable management |
| **Other** | flask-cors | Cross-Origin Resource Sharing |

---

## 🏗️ Project Architecture

NewsLens AI follows a **three-tier architecture** pattern:

### 1. Presentation Layer (Frontend)
- Built with **React + Vite** for a fast, interactive user interface
- Communicates with the backend via HTTP REST API calls
- Renders analysis results in modular card-based components

### 2. Application Layer (Backend)
- **Flask** REST API server handling all business logic
- Routes incoming requests to the appropriate processing modules
- Returns structured JSON responses to the frontend

### 3. Processing Layer (NLP & AI)
- **NLP Pipeline**: Orchestrates preprocessing, sentiment analysis, keyword extraction, and NER
- **LLM Service**: Interfaces with Google Gemini API for summarization and Q&A

### Architecture Flow

```
┌─────────┐     ┌──────────────────┐     ┌──────────────────────┐     ┌─────────────────┐
│         │     │                  │     │                      │     │                 │
│  User   │────▶│  React Frontend  │────▶│   Flask REST API     │────▶│  NLP Pipeline   │
│         │     │  (Vite Dev)      │     │   (Python Backend)   │     │  (NLTK, spaCy,  │
│         │◀────│  Port: 5173      │◀────│   Port: 5000         │     │   YAKE, VADER)  │
│         │     │                  │     │                      │     │                 │
└─────────┘     └──────────────────┘     └──────────┬───────────┘     └─────────────────┘
                                                    │
                                                    │
                                                    ▼
                                          ┌─────────────────┐
                                          │                 │
                                          │  Google Gemini  │
                                          │  API            │
                                          │  (gemini-2.0-   │
                                          │   flash)        │
                                          │                 │
                                          └─────────────────┘
```

> **Note:** The system is **stateless** — no database is required. All analysis is performed on-the-fly per request.

---

## 📁 Folder Structure

```
Project/
├── frontend/                        # React + Vite Frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── Header.jsx           # App header with title and dark mode toggle
│   │   │   ├── ArticleInput.jsx     # Text area for article input with controls
│   │   │   ├── SummaryCard.jsx      # Displays AI-generated summary
│   │   │   ├── SentimentCard.jsx    # Sentiment analysis results with scores
│   │   │   ├── KeywordsCard.jsx     # Top 10 extracted keywords
│   │   │   ├── NERCard.jsx          # Named entities grouped by category
│   │   │   ├── PreprocessingCard.jsx# NLP preprocessing output (tokens, lemmas)
│   │   │   ├── QASection.jsx        # Question answering interface
│   │   │   ├── LoadingOverlay.jsx   # Loading spinner during analysis
│   │   │   └── ReadingStats.jsx     # Word count, reading time statistics
│   │   ├── pages/
│   │   │   └── Dashboard.jsx        # Main dashboard page layout
│   │   ├── App.jsx                  # Root application component
│   │   ├── App.css                  # Application-level styles
│   │   ├── main.jsx                 # React entry point
│   │   └── index.css                # Global styles and CSS variables
│   ├── index.html                   # HTML entry point
│   ├── package.json                 # Node.js dependencies and scripts
│   └── vite.config.js               # Vite configuration
│
├── backend/                         # Python Flask Backend
│   ├── app.py                       # Flask server, routes, error handling
│   ├── preprocess.py                # Text preprocessing (tokenization, lemmatization)
│   ├── sentiment.py                 # VADER sentiment analysis
│   ├── keywords.py                  # YAKE keyword extraction
│   ├── ner.py                       # spaCy Named Entity Recognition
│   ├── nlp_pipeline.py              # Orchestrates all NLP modules
│   ├── llm_service.py               # Google Gemini API integration
│   ├── utils.py                     # Helper/utility functions
│   ├── requirements.txt             # Python dependencies
│   └── .env                         # Environment variables (API key)
│
├── docs/                            # Documentation
│   ├── architecture.md              # System architecture & diagrams
│   ├── ppt_outline.md               # Presentation outline
│   └── report_outline.md            # Project report outline
│
└── README.md                        # This file
```

---

## 📦 Installation & Setup

### Prerequisites

| Requirement | Minimum Version |
|-------------|----------------|
| Node.js | v16.0+ |
| Python | 3.9+ |
| pip | Latest |
| Google Gemini API Key | Free tier available |

### Step 1: Clone or Download the Project

```bash
git clone <repository-url>
cd Project
```

### Step 2: Backend Setup

```bash
# Navigate to backend directory
cd backend

# Install Python dependencies
pip install -r requirements.txt

# Download spaCy English language model
python -m spacy download en_core_web_sm
```

### Step 3: Frontend Setup

```bash
# Navigate to frontend directory
cd frontend

# Install Node.js dependencies
npm install
```

### Step 4: Model Configuration
1. The AI models (`BART` and `DistilBERT`) run locally on your machine for privacy and independence.
2. **Note:** On the first run, the backend will download these models (approx. 2GB) from Hugging Face. This might take a few minutes depending on your internet connection.le `backend/.env`
3. Replace the placeholder with your actual API key:

```env
GEMINI_API_KEY=your_actual_api_key_here
```

> ⚠️ **Important:** Never commit your API key to version control. The `.env` file is excluded via `.gitignore`.

---

## 🚀 Running the Application

### Start the Backend Server

```bash
cd backend
python app.py
```

The Flask server will start at **http://localhost:5000**

You should see output similar to:
```
 * Running on http://127.0.0.1:5000
 * Debug mode: on
```

### Start the Frontend Development Server

Open a **new terminal** and run:

```bash
cd frontend
npm run dev
```

The React application will start at **http://localhost:5173**

You should see output similar to:
```
  VITE v5.x.x  ready in xxx ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: http://xxx.xxx.xxx.xxx:5173/
```

### Access the Application

Open your browser and navigate to **http://localhost:5173**

---

## 📡 API Documentation

The backend exposes two RESTful API endpoints:

### `POST /analyze`

Analyzes a news article and returns comprehensive NLP results.

**Request:**

```http
POST http://localhost:5000/analyze
Content-Type: application/json

{
  "text": "The European Union has approved the AI Act, the world's first comprehensive artificial intelligence regulation. The legislation aims to ensure AI systems used in the EU are safe, transparent, and respect fundamental rights. Companies deploying high-risk AI systems will face strict requirements including risk assessments and human oversight."
}
```

**Response:**

```json
{
  "summary": "The EU has approved the AI Act, the first comprehensive AI regulation globally, requiring AI systems to be safe, transparent, and rights-respecting, with strict requirements for high-risk deployments.",
  "sentiment": {
    "label": "Positive",
    "compound": 0.7269,
    "positive": 0.198,
    "negative": 0.052,
    "neutral": 0.750
  },
  "keywords": [
    { "keyword": "AI Act", "score": 0.0234 },
    { "keyword": "artificial intelligence", "score": 0.0412 },
    { "keyword": "European Union", "score": 0.0523 },
    { "keyword": "regulation", "score": 0.0678 },
    { "keyword": "high-risk AI systems", "score": 0.0712 }
  ],
  "entities": [
    { "text": "European Union", "label": "ORG" },
    { "text": "AI Act", "label": "LAW" }
  ],
  "preprocessing": {
    "original_tokens": ["The", "European", "Union", "..."],
    "filtered_tokens": ["European", "Union", "approved", "..."],
    "lemmatized_tokens": ["European", "Union", "approve", "..."]
  },
  "statistics": {
    "word_count": 52,
    "character_count": 312,
    "sentence_count": 3,
    "reading_time": "1 min"
  }
}
```

---

### `POST /ask`

Answers a question about the provided article using Google Gemini.

**Request:**

```http
POST http://localhost:5000/ask
Content-Type: application/json

{
  "text": "The European Union has approved the AI Act, the world's first comprehensive artificial intelligence regulation...",
  "question": "What requirements do companies face under the AI Act?"
}
```

**Response:**

```json
{
  "answer": "Under the AI Act, companies deploying high-risk AI systems will face strict requirements including mandatory risk assessments and human oversight to ensure safety, transparency, and respect for fundamental rights."
}
```

---

### Error Responses

| Status Code | Description |
|-------------|-------------|
| `400` | Missing or empty `text` field in request body |
| `500` | Internal server error (e.g., API key issue, model error) |

**Example Error Response:**

```json
{
  "error": "No text provided for analysis"
}
```

---

## 📰 Sample Test Data

Use the following sample article to test the system:

> **EU AI Act — A Landmark Regulation**
>
> The European Union has officially approved the Artificial Intelligence Act, making it the world's first comprehensive legal framework for AI regulation. The legislation, which was proposed by the European Commission in April 2021, underwent extensive negotiations before being finalized in December 2023.
>
> The AI Act establishes a risk-based approach to regulating artificial intelligence. It categorizes AI systems into four risk levels: unacceptable risk, high risk, limited risk, and minimal risk. AI systems deemed to pose unacceptable risks, such as social scoring by governments and real-time biometric surveillance in public spaces, are banned outright.
>
> High-risk AI systems, including those used in critical infrastructure, education, employment, law enforcement, and migration management, must meet stringent requirements. These include conducting conformity assessments, maintaining detailed technical documentation, ensuring human oversight, and implementing robust data governance practices.
>
> The regulation also addresses general-purpose AI models, including large language models like GPT-4 and Google's Gemini. Providers of these foundation models must comply with transparency obligations, including disclosing that content was generated by AI and publishing summaries of copyrighted training data.
>
> The European Parliament approved the final text with an overwhelming majority of 523 votes in favor, 46 against, and 49 abstentions. European Commission President Ursula von der Leyen praised the legislation as a "global first" that would set international standards for trustworthy AI.
>
> The AI Act includes significant penalties for non-compliance. Companies violating the ban on prohibited AI practices face fines of up to 35 million euros or 7% of their global annual turnover, whichever is higher. For other violations, fines can reach up to 15 million euros or 3% of global turnover.
>
> Industry reactions have been mixed. While many technology companies and trade associations have expressed support for regulatory clarity, some have raised concerns about compliance costs and the potential impact on innovation. The Act provides a transition period of up to 36 months for full implementation, giving companies time to adapt their AI systems and processes.
>
> The AI Act is expected to influence AI regulation globally, similar to how the General Data Protection Regulation (GDPR) set the standard for data privacy laws worldwide. Several countries, including Brazil, Canada, and Japan, are already developing their own AI governance frameworks with reference to the EU's approach.

---

## 📦 Modules Description

### Backend Modules

| Module | File | Description |
|--------|------|-------------|
| **Flask Server** | `app.py` | Main application entry point. Defines REST API routes (`/analyze`, `/ask`), handles request validation, error handling, and CORS configuration. Orchestrates calls to NLP and LLM modules. |
| **Preprocessing** | `preprocess.py` | Text preprocessing pipeline using NLTK. Performs tokenization (word-level splitting), stopword removal (filtering common English words), and lemmatization (reducing words to base form). Returns original tokens, filtered tokens, and lemmatized tokens. |
| **Sentiment Analysis** | `sentiment.py` | Sentiment analysis using NLTK's VADER (Valence Aware Dictionary and sEntiment Reasoner). Computes compound, positive, negative, and neutral scores. Classifies overall sentiment as Positive, Negative, or Neutral based on compound score thresholds. |
| **Keyword Extraction** | `keywords.py` | Keyword extraction using the YAKE (Yet Another Keyword Extractor) algorithm. Extracts top 10 keywords/keyphrases ranked by relevance score. YAKE is unsupervised and does not require training data. |
| **Named Entity Recognition** | `ner.py` | Named Entity Recognition using spaCy's `en_core_web_sm` model. Identifies and categorizes entities such as persons (PERSON), organizations (ORG), locations (GPE), dates (DATE), monetary values (MONEY), and more. |
| **NLP Pipeline** | `nlp_pipeline.py` | Orchestration module that coordinates all NLP processing modules. Calls preprocessing, sentiment analysis, keyword extraction, and NER in sequence, then assembles the combined results into a unified response object. |
| **LLM Service** | `llm_service.py` | Integration layer for Google Gemini API. Handles API key configuration, model initialization (`gemini-2.0-flash`), prompt engineering for summarization and question answering, and response parsing. |
| **Utilities** | `utils.py` | Helper functions including text statistics computation (word count, character count, sentence count, estimated reading time) and other shared utility operations. |

### Frontend Components

| Component | File | Description |
|-----------|------|-------------|
| **App** | `App.jsx` | Root component managing global state and theme |
| **Dashboard** | `Dashboard.jsx` | Main page layout orchestrating all analysis components |
| **Header** | `Header.jsx` | Application header with logo, title, and dark mode toggle |
| **ArticleInput** | `ArticleInput.jsx` | Text area with paste, sample load, and clear controls |
| **SummaryCard** | `SummaryCard.jsx` | Displays AI-generated summary with copy functionality |
| **SentimentCard** | `SentimentCard.jsx` | Visual sentiment analysis with score bars |
| **KeywordsCard** | `KeywordsCard.jsx` | Keyword tags with relevance scores |
| **NERCard** | `NERCard.jsx` | Named entities grouped and color-coded by type |
| **PreprocessingCard** | `PreprocessingCard.jsx` | Shows tokenization, filtering, and lemmatization output |
| **QASection** | `QASection.jsx` | Interactive Q&A interface for article-grounded questions |
| **LoadingOverlay** | `LoadingOverlay.jsx` | Full-screen loading spinner during analysis |
| **ReadingStats** | `ReadingStats.jsx` | Reading statistics (word count, time estimate) |

---

## 🔮 Future Improvements

- 🌐 **Multi-Language Support** — Extend NLP processing to support Hindi, Spanish, French, and other languages
- 🔗 **Article URL Input** — Accept URLs and automatically scrape article content using web scraping
- 📦 **Batch Article Processing** — Analyze multiple articles simultaneously with comparative insights
- 📄 **Export as PDF Report** — Generate downloadable PDF reports of the complete analysis
- 👤 **User Authentication & History** — Save past analyses with user accounts for future reference
- ⚖️ **Article Comparison** — Side-by-side comparison of sentiment, keywords, and entities across articles
- 🏷️ **Topic Classification** — Automatically categorize articles into topics (Politics, Sports, Tech, etc.)
- 🔊 **Text-to-Speech Summary** — Listen to the generated summary using browser speech synthesis API
- 📊 **Visualization Enhancements** — Word clouds, sentiment trend charts, and entity relationship graphs
- 🔌 **News API Integration** — Fetch trending articles directly from news APIs for instant analysis

---

## 📝 License

This project was developed as an academic project.

---

<p align="center">
  Made with ❤️ using React, Flask, and Google Gemini
</p>
