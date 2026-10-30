# PhishShield — Intelligent Phishing Detection and Cyber Threat Analysis System

> **"Detect Suspicious Signals. Understand the Risk. Browse Smarter."**  
> An Academic Information Security Project developed as a University Computer Science Capstone.

---

## 🛡️ Project Overview

**PhishShield** is an explainable, defensive cyber threat analysis platform engineered to evaluate suspicious URLs and email communications. Unlike black-box detection tools or dynamic execution sandboxes that risk Server-Side Request Forgery (SSRF), PhishShield utilizes **deterministic, isolated heuristic analysis**.

Every analysis output includes:
- A transparent risk score (0 to 100) and clear assessment category.
- Specific triggered security rule identifiers (e.g. `URL_IP_HOSTNAME`, `EMAIL_URGENCY_THREAT`).
- Human-readable threat explanations and the exact empirical evidence observed.
- Actionable defense recommendations for end users and security analysts.

---

## 🚀 Key Features

1. **RFC 3986 Safe URL Threat Analyzer:**
   - Isolated in-memory evaluation without connecting to or visiting candidate links (Zero SSRF).
   - Numeric IP hostname detection (IPv4 / IPv6).
   - Punycode & IDN homograph attack inspection (`xn--` markers).
   - Public URL shortener obfuscation shield (`bit.ly`, `tinyurl.com`, `t.co`, etc.).
   - Deceptive authority userinfo `@` syntax detection (`http://brand.com@attacker.com`).
   - Deep subdomain chaining and brand impersonation heuristics.
   - Dangerous executable payload link detection (`.exe`, `.scr`, `.bat`, `.iso`).

2. **Social Engineering Email Phishing Analyzer:**
   - Artificial time pressure and account suspension ultimatums.
   - Credential harvesting prompts (passwords, PINs, SSNs).
   - Unsolicited lottery, prize, and financial windfall lures.
   - Irreversible cryptocurrency and retail gift card payment demands.
   - Recursive inspection of embedded URLs within email text.

3. **User Authentication & Granular Access Control:**
   - Secure password hashing using PBKDF2/scrypt with per-user cryptographic salts.
   - Signed JSON Web Token (JWT) session handling with rate limiting on login/registration.
   - Strict Insecure Direct Object Reference (IDOR) prevention enforcing record ownership.
   - User account deletion with relational cascade purging.

4. **Privacy-Conscious Data Storage:**
   - Sensitive URL query parameters (such as `token`, `password`, `key`) are automatically redacted prior to database persistence.
   - Email text is never stored in full; only the subject line or an 80-character snippet is retained.

5. **Security Awareness Center & Phishing IQ Quiz:**
   - 10 structured educational modules explaining modern phishing methods and defenses.
   - Interactive scenario-based quiz with instant grading and in-depth explanations.

6. **Real-Time Security Test Matrix:**
   - In-browser interactive execution of benchmark test cases reporting pass/fail outcomes and execution runtimes in milliseconds.
   - Comprehensive automated backend test suite (36 tests via Pytest).

---

## 🏗️ Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 18, TypeScript 5, Vite, Tailwind CSS, Lucide React icons, Recharts |
| **Backend** | Python 3.14 / 3.10+, Flask 3.1, Flask-SQLAlchemy, Werkzeug Security, Flask-Limiter, PyJWT |
| **Database** | SQLite with SQLAlchemy ORM (local development) |
| **Testing** | Pytest 9.2 automated test suite |

---

## 💻 Quick Start Guide for Windows

### Prerequisites
- Python 3.10+ (tested on Python 3.14)
- Node.js v18+ and npm (tested on Node v24.19 and npm 11.17)

### 1. Clone or Open Workspace
Open PowerShell in the project directory:
```powershell
cd "c:\Users\Admin\Downloads\New folder"
```

### 2. Backend Setup
```powershell
# Navigate to backend and create virtual environment
cd backend
python -m venv venv

# Install backend dependencies
.\venv\Scripts\pip.exe install -r requirements.txt
cd ..
```

### 3. Frontend Setup
```powershell
# Navigate to frontend and install npm packages
cd frontend
npm.cmd install
cd ..
```

---

## 🏃 Running the Application

PhishShield requires two terminal windows running concurrently:

### Terminal 1: Backend API Server
```powershell
& ".\backend\venv\Scripts\python.exe" backend\run.py
```
*API runs on `http://127.0.0.1:5000`*

### Terminal 2: Frontend Client
```powershell
cd frontend
npm.cmd run dev
```
*Web application opens on `http://localhost:5173`*

Open **`http://localhost:5173`** in your browser to access the PhishShield application.

---

## 🧪 Running Automated Tests

### Backend Test Suite (Pytest)
```powershell
cd backend
.\venv\Scripts\pytest.exe -v
```
*Expected: 36 passed in ~3s.*

### Frontend Production Build Test
```powershell
cd frontend
npm.cmd run build
```
*Expected: Vite builds successfully with zero TypeScript errors.*

---

## 📁 Project Directory Structure

```
PhishShield/
├── backend/
│   ├── app/
│   │   ├── config.py             # Environment configuration
│   │   ├── extensions.py         # DB, Limiter, CORS singletons
│   │   ├── models/               # SQLAlchemy DB models (User, Scan, Finding, Event)
│   │   ├── routes/               # REST API blueprints (Auth, Analyze, Scans, Stats, Quiz, Tests)
│   │   ├── services/             # URL Analyzer, Email Analyzer, Explanation Engine, Sanitizer
│   │   └── security/             # Password hashing, JWT helpers, rate limits
│   ├── tests/                    # 36 automated unit & integration tests
│   ├── run.py                    # Server entry point (port 5000)
│   ├── requirements.txt
│   └── .env.example
├── frontend/
│   ├── src/
│   │   ├── components/           # Reusable UI components (ScoreMeter, RiskBadge, FindingCard, Modal)
│   │   ├── context/              # AuthContext for session management
│   │   ├── layouts/              # PublicLayout & DashboardLayout (responsive sidebar)
│   │   ├── pages/                # Landing, Auth, Dashboard, Analyzers, History, Quiz, Matrix
│   │   ├── services/             # Axios API client
│   │   └── types/                # TypeScript interfaces
│   ├── package.json
│   ├── vite.config.ts
│   └── tailwind.config.js
├── docs/
│   ├── project-report.md         # Full academic capstone project report
│   ├── architecture.md           # System design & Mermaid diagrams
│   ├── test-plan.md              # Test matrix with actual execution outcomes
│   ├── user-guide.md             # Operational walkthrough and setup manual
│   └── viva-questions.md         # 14 university defense Q&A
├── README.md
└── .gitignore
```

---

## ⚖️ Responsible Use & Academic Disclaimer

PhishShield is developed strictly as an educational cyber threat analysis system. It employs transparent, deterministic heuristics to identify suspicious markers. It does **not** replace commercial endpoint security software, nor does it guarantee that any website is safe. Users should always exercise personal vigilance when clicking links or providing confidential information.
