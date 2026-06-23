# 🎓 IQRA VERIFY

### Official Degree & Transcript Authentication, Verification & Attestation Platform
**Iqra University · Powered by ARIA OCR Intelligence**

[Student Portal](#-portals) · [Verification Portal](#-portals) · [Admin Portal](#-portals) · [ARIA Agent](#-aria-ai-agent)

</div>

---

## 📋 Overview

**IQRA VERIFY** is a full-stack academic credential authentication platform built for Iqra University. It enables students to apply for degree and transcript attestation, while administrators and third-party verifiers can cryptographically validate the authenticity of issued credentials.

The system leverages **Google Gemini AI** (via the ARIA engine) to automate OCR-based document scanning, fraud detection, and payment receipt verification — combining AI intelligence with SHA-256 cryptographic sealing to produce tamper-proof attestation records.

---

## ✨ Features

### 🧑‍🎓 Student Portal
- Secure student registration and login
- Step-by-step attestation application workflow
- Document upload (CNIC, Matric, Inter, Transcript, Degree)
- AI-powered payment receipt OCR (screenshot upload)
- Credit card and crypto payment simulation
- Real-time application status tracking

### 🔍 Verification Portal (Public)
- Public credential lookup via Roll No, Registration No, or SHA-256 hash
- QR code-based verification support
- Instant authenticity check against the university registrar database
- Cryptographic hash display for verified credentials

### 🛡️ Admin Portal (Registrar / Verification Officer)
- Dual-role admin login (Registrar & Verification Officer)
- Application review with approval / rejection workflow
- Manual cryptographic signing and SHA-256 attestation seal generation
- **ARIA Autopilot Sweep** — automated bulk review and approval
- Fraud alert management with severity classification (High / Medium / Low)
- Full audit log viewer with actor, role, timestamp, and action status
- System analytics dashboard

### 🤖 ARIA AI Agent
- Conversational chatbot powered by Gemini AI
- Answers queries about application status, university policies, and platform features
- Context-aware responses grounded in live platform data
- Graceful fallback to mock intelligence when API key is unavailable

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                      React Frontend                      │
│  App.tsx → StudentPortal | VerificationPortal |          │
│            AdminPortal | AriaAgent                       │
└────────────────────────┬────────────────────────────────┘
                         │ REST API (Express)
┌────────────────────────▼────────────────────────────────┐
│                   server.ts (Express)                    │
│                                                          │
│  /api/auth        → Student & Admin auth                 │
│  /api/applications → CRUD for attestation apps           │
│  /api/ocr/process → Gemini OCR + fraud detection         │
│  /api/payment/*   → Receipt OCR + payment verification   │
│  /api/public-verify → Public SHA-256 hash lookup         │
│  /api/admin/*     → ARIA Autopilot, analytics, audit     │
│  /api/aria/chat   → ARIA conversational agent            │
│  /api/system/*    → Audit logs & system analytics        │
└────────────────────────┬────────────────────────────────┘
                         │
         ┌───────────────┼───────────────┐
         │               │               │
   ┌─────▼──────┐ ┌──────▼─────┐ ┌──────▼──────┐
   │  In-Memory │ │ Google     │ │ Node.js     │
   │  Database  │ │ Gemini AI  │ │ crypto      │
   │ (mockDb.ts)│ │ (GenAI SDK)│ │ (SHA-256)   │
   └────────────┘ └────────────┘ └─────────────┘
```

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, TypeScript, Tailwind CSS v4 |
| Backend | Node.js, Express 4, TypeScript (`tsx`) |
| AI / OCR | Google Gemini (`gemini-3.5-flash`) via `@google/genai` |
| Cryptography | Node.js `crypto` (SHA-256 hashing) |
| Build Tool | Vite 6 |
| Animation | Motion (Framer Motion) |
| Icons | Lucide React |

---

## 🚀 Getting Started

### Prerequisites
- **Node.js** v18 or higher
- A **Google Gemini API key** ([get one free at Google AI Studio](https://aistudio.google.com))

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/iqra-verify.git
cd iqra-verify

# 2. Install dependencies
npm install

# 3. Configure environment variables
cp .env.example .env.local
# Edit .env.local and set your GEMINI_API_KEY
```

### Running Locally

```bash
npm run dev
```

The app runs on **http://localhost:3000**.

> **Note:** If no valid `GEMINI_API_KEY` is provided, ARIA falls back to high-fidelity mock intelligence automatically — the platform remains fully functional.

### Production Build

```bash
npm run build
npm start
```

---

## 🔑 Demo Credentials

### Student Accounts

| Email | Password | Roll No |
|---|---|---|
| kamran@iqra.edu.pk | iqra123 | IU-BSCS-2022-045 |
| ayesha@iqra.edu.pk | iqra123 | IU-BBA-2021-120 |
| zainab@iqra.edu.pk | iqra123 | IU-BSSE-2022-094 |
| bilal@iqra.edu.pk | iqra123 | IU-MSSE-2023-012 |

### Admin Accounts

| Email | Password | Role |
|---|---|---|
| registrar@iqra.edu.pk | iqraAdminPass | Registrar |
| verification@iqra.edu.pk | iqraAdminPass | Verification Officer |

---

## 🔐 Cryptographic Verification

Approved attestations are sealed with a **SHA-256 hash** derived from the student's Roll No, Registration No, and approval timestamp:

```
SHA-256(rollNo | regNo | timestamp | approvedBy)
```

This hash is stored with the application and can be used for **public verification** at any time via the Verification Portal — no login required.

---

## 📁 Project Structure

```
├── server.ts                  # Express backend (API routes, AI logic, crypto)
├── src/
│   ├── App.tsx                # Root component & routing
│   ├── main.tsx               # React entry point
│   ├── types.ts               # Shared TypeScript types & enums
│   ├── index.css              # Global styles
│   ├── data/
│   │   └── mockDb.ts          # Seed data (students, applications, fraud alerts)
│   └── components/
│       ├── StudentPortal.tsx  # Student-facing UI
│       ├── VerificationPortal.tsx  # Public verifier UI
│       ├── AdminPortal.tsx    # Admin/Registrar dashboard
│       └── AriaAgent.tsx      # ARIA conversational chatbot
├── index.html
├── vite.config.ts
├── tsconfig.json
├── package.json
└── .env.example
```

---

## 🤖 ARIA Fraud Detection

ARIA's document OCR pipeline detects the following fraud indicators:

- **Signature Mismatch** — signature on uploaded document differs from official records
- **Photoshop Manipulation** — visual integrity failure detected in document image
- **Metadata Mismatch** — document metadata inconsistent with submission date
- **CGPA Alteration** — extracted GPA does not match the official registrar database
- **Duplicate Submission** — same document submitted across multiple applications
- **Anomalous Record** — unusual patterns flagged by AI analysis

Fraud alerts are classified by severity (High / Medium / Low) and tracked in the Admin Portal.

---

## 📜 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for details.

---


Built with ❤️ for **Iqra University** · Karachi, Pakistan

</div>
