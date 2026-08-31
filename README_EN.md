# FaceTomato · AI-Powered Resume Analysis and Mock Interview System

[简体中文](./README.md) | English

<div align="center">

<img src="./assets/facetomato_new.jpg" alt="FaceTomato preview" width="880" />

[![GitHub stars](https://img.shields.io/github/stars/Infinityay/FaceTomato?style=flat-square)](https://github.com/Infinityay/FaceTomato/stargazers)
[![Frontend](https://img.shields.io/badge/Frontend-React%2018%20%2B%20TypeScript-blue?style=flat-square)]()
[![Backend](https://img.shields.io/badge/Backend-FastAPI%20%2B%20LangChain-green?style=flat-square)]()
[![Storage](https://img.shields.io/badge/Storage-SQLite%20%2B%20Local%20Index-orange?style=flat-square)]()
[![License](https://img.shields.io/github/license/Infinityay/FaceTomato?style=flat-square)](https://github.com/Infinityay/FaceTomato/blob/main/LICENSE)

</div>

---

## ✨ Overview

**FaceTomato** is an AI assistant for technical job seekers. It currently supports frontend, backend, and mobile development; product management; speech algorithms; LLM application development; LLM algorithms; search, advertising, and recommendation algorithms; game development; risk-control algorithms; and more. It covers the complete workflow from application preparation to interview practice, with features including:

- Resume parsing
- Job description matching
- Resume optimization
- Interview-experience question search
- Mock interviews
- Interview reviews
- Voice-assisted answering

> The tomato is FaceTomato's visual and brand motif: lightweight yet valuable, approachable yet powerful.
> We want FaceTomato to provide the crucial assist in your job search:
> **🍅 Powerful support behind a simple appearance, helping you perform reliably when it matters most.**

## ⚡ Quick Start

FaceTomato can be started from source or with Docker.

### 1. Run from source

#### Start the backend

```bash
cd backend
uv sync
cp .env.example .env
```

To explicitly enable local RAG retrieval or build an index, install the optional `rag` dependencies. The current local dependency set targets non-Windows platforms. On Windows, we recommend Docker, a Linux environment, or the non-RAG fallback.

```bash
cd backend
uv sync --extra rag
```

Complete `backend/.env` with your settings, then start the backend:

```bash
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 6522
```

The API documentation will be available at `http://127.0.0.1:6522/docs`.

#### Start the frontend

```bash
cd frontend
npm install
npm run dev
```

The frontend is available at `http://127.0.0.1:5569` by default.

### 2. Run with Docker

Before the first run, prepare the backend environment file:

```bash
cp backend/.env.example backend/.env
```

Then run the following command from the project root:

```bash
docker compose up --build -d
```

To build a RAG-capable backend image, explicitly enable the build-time installation option:

```bash
BACKEND_INSTALL_RAG=true docker compose up --build -d
```

Then enable RAG at runtime in `backend/.env`:

```env
MOCK_INTERVIEW_RAG=true
```

The frontend is available at `http://127.0.0.1:5569` by default.

## 🚀 Core Features

### 1. 📄 Resume Parsing

Upload resumes in PDF, DOCX, PNG/JPG, or TXT format and automatically extract structured information.

### 2. 🎯 Job Description Matching

Enter a job description to extract requirements such as skills, education, experience, and responsibilities, then generate a match assessment based on the resume.

### 3. ✍️ Resume Optimization

Choose between general optimization and job-specific optimization to improve wording, structure, and keyword coverage.

### 4. 📚 Interview Question Search

Search interview-experience questions stored in SQLite, with pagination, filters, statistics, and adjacent-item navigation.

### 5. 🎙️ Mock Interviews

Practice with SSE-streamed sessions, Markdown-rendered conversations, multi-turn follow-up questions, local frontend snapshot recovery, and continued context.

### 6. 📝 Interview Reviews

Generate structured review reports from mock interviews to identify opportunities to improve delivery, content, and answering strategies.

## 📦 Requirements

- Node.js >= 18
- npm >= 9
- Python >= 3.12, < 3.13
- uv

## 📚 Preparing Interview Data (Required Reading)

Interview question data is **not** committed to this repository, and `backend/data/` is excluded by `.gitignore`.

To browse real interview-experience questions in FaceTomato, first prepare `backend/data/interviews.db`. See [`docs/interview-data.md`](./docs/interview-data.md) for complete instructions (currently in Chinese), including:

- The `backend/data/` directory layout
- How to obtain `interviews.db`
- Requirements for the raw JSON data directory
- How to use the migration script
- Optional steps for building the local RAG index

## ⚙️ Configuration

The main references for configuration and retrieval features are:

- `backend/.env.example`
- `docs/README.md`
- `docs/backend/configuration.md`
- `docs/backend/rag-config.md`

## 🛠️ Runtime Settings

The frontend can override the backend defaults for each request. The primary fields are:

- LLM: `apiKey`, `baseURL`, `model`
- OCR: `ocrApiKey`
- Speech: `speechAppKey`, `speechAccessKey`

## 🗂️ Building the Interview Index

Before building the index, prepare `backend/data/interviews.db` as described in [`docs/interview-data.md`](./docs/interview-data.md).

Then install the optional `rag` dependencies (the current local dependency set targets non-Windows platforms) and build the index:

```bash
cd backend
uv sync --extra rag
uv run python scripts/build_interview_zvec_index.py
```

## 🤝 Contributing

Issues and pull requests are welcome.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for the contribution workflow, TDD requirements, commit conventions, and pull request guidelines.

## ⚠️ Disclaimer

Analysis results, optimization suggestions, and mock interview content generated by this project are for reference only and do not guarantee any recruitment outcome.

Users are responsible for ensuring that uploaded resumes, job descriptions, and related data are lawful, accurate, and compliant.

When the project integrates third-party model, speech, or retrieval services, those providers are responsible for the availability, accuracy, and compliance of their respective services.

Except for rights expressly granted by the `LICENSE`, third-party data, assets, model services, and their outputs may be subject to their own terms.

The developers are not liable for direct or indirect losses arising from use of this project.

## 📄 License

This project is released under the **GNU Affero General Public License v3.0 (AGPL-3.0)**. You may use, modify, and redistribute it under the terms of the AGPL-3.0. When distributing the project or a modified version, you must provide the corresponding source code as required by the license. If you make a modified version available to users over a network, you must also provide those remote users with a way to obtain its corresponding source code.

See the repository's [LICENSE](./LICENSE) file for the authoritative terms.

## Acknowledgements

- Thanks to [zvec](https://zvec.org/) for making it easy to add RAG capabilities to this project.

- Thanks to the members of the [LinuxDo](https://linux.do/) community for generously sharing their knowledge, which has been tremendously helpful during development.
