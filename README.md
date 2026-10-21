# TATHYA — Secure Document Management System

**A secure, intelligent platform for document storage, integrity verification, case management, and AI-powered retrieval.**

TATHYA is a document management platform designed to keep sensitive records organized, secure, traceable, and easy to retrieve. It combines secure file storage, cryptographic integrity verification, blockchain-based proof, version control, and an AI-powered assistant in one system.

## Key Features

- **Secure Document Storage:** Store documents in private object storage with controlled access.
- **Case Management:** Organize documents around cases and their authorized members.
- **Role-Based Access Control:** Restrict operations according to user roles and permissions.
- **Document Versioning:** Maintain previous versions instead of silently overwriting files.
- **SHA-256 Integrity Verification:** Generate cryptographic hashes to detect file modifications.
- **Blockchain Verification:** Anchor document hashes on a blockchain for tamper-evident verification.
- **Audit Trail:** Maintain a record of important actions for traceability.
- **OCR and Full-Text Search:** Extract text from supported documents and search their contents.
- **AI-Powered Document Assistant:** Retrieve relevant information from authorized documents and provide answers with source references.

## Architecture

```text
Next.js Frontend
       |
       v
FastAPI Backend
       |
       +---- PostgreSQL + pgvector
       |     Metadata, users, cases,
       |     document versions, embeddings
       |
       +---- MinIO
       |     Private document storage
       |
       +---- OCR and Search
       |     Text extraction and retrieval
       |
       +---- AI / RAG
       |     Context-aware question answering
       |
       +---- Ethereum / Hardhat
             Document hash verification
```

**Integrity design:** Document files remain in private storage. PostgreSQL maintains their metadata, while SHA-256 hashes can be anchored on the blockchain. The blockchain stores verification data, not the original documents.

## Technology Stack

| Component | Technologies |
|---|---|
| Frontend | Next.js, React, TypeScript, Tailwind CSS |
| Backend | Python, FastAPI, SQLAlchemy, Pydantic |
| Database | PostgreSQL, pgvector |
| Object Storage | MinIO |
| Authentication | JWT, bcrypt |
| Blockchain | Solidity, Hardhat, Ethereum-compatible network |
| Document Processing | Tesseract OCR, PyMuPDF |
| AI and Retrieval | LLMs, embeddings, RAG |
| Infrastructure | Docker Compose |

## Project Structure

```text
TATHYA/
├── frontend/       # Web application
├── backend/        # APIs, authentication and business logic
├── blockchain/     # Smart contracts and deployment scripts
├── docs/           # Technical documentation
└── docker/         # Infrastructure configuration
```

## Getting Started

### Prerequisites

- Python 3.11+
- Node.js and npm
- Docker Desktop
- Tesseract OCR (optional, for scanned documents)
- Ollama or another supported LLM provider, if using the AI assistant

### 1. Configure environment variables

Create your local environment file from the provided example:

```powershell
Copy-Item .env.example .env
```

Configure the required database, storage, authentication, blockchain, and AI settings in the appropriate environment files. Never commit real credentials or private keys.

### 2. Start infrastructure

```powershell
docker compose -f docker/docker-compose.yml up -d
```

### 3. Start the backend

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\pip install -r requirements.txt
.\.venv\Scripts\uvicorn app.main:app --reload --port 8000
```

API documentation: `http://localhost:8000/docs`

### 4. Start the frontend

Open another terminal:

```powershell
cd frontend
npm install
npm run dev
```

Open the application at `http://localhost:3000`.

### 5. Configure blockchain and AI services

Follow the project configuration and documentation to deploy the integrity smart contract to your development blockchain and configure the contract address. Configure the selected LLM provider before using AI-powered retrieval.

## Security Notes

- Keep environment files, API keys, private keys, and production credentials out of version control.
- Use fictional demo data; do not upload real confidential records to an unapproved environment.
- Restrict document access through backend authorization checks.
- Treat blockchain verification as an integrity mechanism, not as a replacement for access control or secure storage.
- Configure production-grade authentication, monitoring, backups, and deployment security before production use.

## Project Status

TATHYA is a software prototype demonstrating secure document management, traceability, integrity verification, search, and AI-assisted retrieval. Production deployment requires environment-specific security review, testing, and operational hardening.
