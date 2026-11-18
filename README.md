# 🛡️ PhishGuard - AI-Assisted Phishing Detection Platform

PhishGuard is a cybersecurity platform that analyzes **emails, URLs, and images** for phishing indicators and social engineering red flags. It provides a **0-100 risk score** along with plain-English explanations, helping users understand *why* something is suspicious instead of relying on a black-box prediction.

The platform includes both a **web dashboard** and a **Chrome extension**, powered by a shared backend for consistent threat analysis.

---

## 🎯 Problem Statement

Phishing remains one of the most common and successful cyberattacks because attackers exploit human psychology rather than technical vulnerabilities.

Domains such as `paypa1.com` can closely resemble legitimate websites like `paypal.com`, while urgency-driven messages such as *"Your account will be suspended within 24 hours"* are designed to pressure users into making unsafe decisions.

Identifying these threats manually can be difficult, especially under time pressure.

---

## ✅ Solution

PhishGuard automates the verification process by detecting common phishing patterns and presenting clear explanations for every risk indicator.

Instead of simply labeling content as safe or unsafe, the platform highlights the factors contributing to the risk score, enabling users to make informed security decisions.

---

## ✨ Features

### 📧 Email Analysis

- Sender spoofing detection
- Brand impersonation detection
- Urgency, fear, authority, and reward-based language analysis
- Credential request detection
- Embedded URL extraction and scanning
- HTML link verification against actual destinations

### 🌐 URL Analysis

- Typosquatting detection using Levenshtein distance
- Homoglyph attack detection (`paypa1.com`, `rnicrosoft.com`)
- Brand names hidden inside subdomains
- Suspicious top-level domain (TLD) detection
- Raw IP address detection
- URL shortener identification
- Non-HTTPS link detection

### 🖼️ Media Forensics (Experimental)

- EXIF metadata inspection
- Error Level Analysis (ELA)
- Basic image manipulation indicators

### 🤖 AI-Assisted Review

- Optional Gemini-powered tone and intent analysis
- Complements rule-based detection
- Provides a second opinion for ambiguous cases

### 🔌 Chrome Extension

- Live risk badge for Gmail messages
- Visual warnings on suspicious hyperlinks
- One-click security scans through popup interface

---

## 🎓 Key Contributions

- Designed and implemented a rule-based phishing detection engine.
- Developed a React-based cybersecurity dashboard for threat analysis.
- Built a Chrome extension for real-time phishing awareness.
- Integrated Google Gemini for AI-assisted content evaluation.
- Implemented image forensic techniques including EXIF inspection and Error Level Analysis.
- Created an explainable risk scoring system that provides transparent security findings.

---

## 🏗️ System Architecture

```
 Web Application (React) ──┐
                           ├──▶ Backend (Node.js / Express)
 Chrome Extension ─────────┘             │
                                         ▼
                         Email / URL / Media Analysis Engine
                                         │
                                         ▼
                           Gemini API (Optional)
```

---

## 📡 API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|----------|
| `/api/analyze/email` | POST | Analyze email content |
| `/api/analyze/url` | POST | Analyze URLs |
| `/api/analyze/media` | POST | Analyze uploaded images |

### Risk Levels

| Score | Risk Level |
|---------|---------|
| 0-34 | Low |
| 35-69 | Medium |
| 70-100 | High |

---

## 🤖 How AI Is Used

PhishGuard follows a **hybrid detection approach**.

The rule-based engine serves as the primary detection mechanism and generates the core risk score along with detailed explanations.

When a `GEMINI_API_KEY` is configured, Gemini evaluates the tone, intent, and persuasive tactics present in email content. The final assessment combines:

- **65% Heuristic Analysis**
- **35% AI Evaluation**

This weighting is a design decision intended to prioritize explainability while leveraging AI for additional context.

The platform remains fully operational even when AI is disabled.

---

## 🧰 Technology Stack

### Frontend
- React 18
- Vite
- Tailwind CSS

### Backend
- Node.js
- Express.js

### Browser Extension
- Chrome Extension (Manifest V3)

### AI & Analysis
- Google Gemini API
- sharp
- exifr

### File Handling
- Multer

---

## 🚀 Getting Started

### Backend

```bash
cd backend
npm install
cp .env.example .env
npm start
```

Runs on:

```text
http://localhost:5001
```

Optional:

```env
GEMINI_API_KEY=your_key_here
```

### Web Application

```bash
cd web-app
npm install
npm run dev
```

Open:

```text
http://localhost:5173
```

### Chrome Extension

1. Open `chrome://extensions`
2. Enable **Developer Mode**
3. Click **Load Unpacked**
4. Select the `extension/` directory
5. Ensure the backend is running

---

## 🧪 Sample URL Analysis Request

```bash
curl -X POST http://localhost:5001/api/analyze/url \
-H "Content-Type: application/json" \
-d '{"url":"http://secure-paypa1-login.verify-account.xyz"}'
```

Expected findings include:

- Character substitution
- Suspicious TLD usage
- Non-HTTPS protocol
- Elevated phishing risk score

---

## ⚠️ Limitations

- The system is primarily heuristic-based and may be evaded by sophisticated attackers.
- The known-brand database is intentionally limited and not exhaustive.
- Image analysis identifies signs of editing but does not confirm deepfake content.
- Gmail detection relies on current Gmail DOM structures and may require updates.
- Automated test coverage has not yet been implemented.

---

## 🔮 Future Enhancements

- Train a machine learning classifier using labeled phishing datasets.
- Integrate CNN-based image analysis for advanced media verification.
- Develop a comprehensive automated testing suite.
- Improve brand and domain coverage.
- Add threat intelligence feed integrations.
- Track and evaluate cases where AI and heuristics disagree.

---

## 📁 Project Structure

```text
phishguard/
├── backend/      # Express API and analysis engine
├── web-app/      # React frontend dashboard
└── extension/    # Chrome Extension (Manifest V3)
```

---

## 👩‍💻 Author

**Harshini Gadhamsetty**

B.E. Computer Science & Engineering (Cyber Security)  
R.M.D Engineering College

GitHub: https://github.com/gadhamsettyharshini

---

## ⭐ Support

If you found this project useful, consider giving it a star.
Contributions, suggestions, and security-related feedback are always welcome.
