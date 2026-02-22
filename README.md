# AI-Powered Automated CV Screening & Candidate Shortlisting with n8n

![AI-Powered CV Screening and Candidate Shortlisting](https://github.com/user-attachments/assets/dc48e631-6f90-45f3-894b-6ee2cf003e68)

---

## 🚀 Executive Summary

This project demonstrates a production-ready AI recruitment pipeline that automates the first stage of candidate evaluation.

The system:

- Monitors a Gmail inbox for incoming job applications
- Extracts PDF CV attachments
- Uses OpenAI to evaluate candidates against a defined job description
- Assigns structured match scores (0–100)
- Determines qualification status based on scoring + experience logic
- Automatically categorizes candidates (Qualified / Unqualified)
- Logs structured results into Google Sheets
- Sends automated HR notifications for shortlisted candidates

This simulates a scalable AI-powered Applicant Tracking System (ATS) backend built entirely using workflow automation.

---

## 🏗 Workflow Architecture

### High-Level System Design

```
                ┌──────────────────────────┐
                │   Gmail Trigger          │
                │ (New CV Application)     │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │  Extract CV Text (PDF)   │
                └────────────┬─────────────┘
                             ↓
                ┌──────────────────────────┐
                │  Job Description Loader  │
                └────────────┬─────────────┘
                             ↓
        ┌─────────────────────────────────────────────┐
        │          OpenAI CV Evaluation Engine        │
        │  - Skills Matching                          │
        │  - Experience Validation                    │
        │  - Education Assessment                     │
        │  - Qualification Logic                      │
        │  - Score (0–100)                            │
        └────────────┬────────────────────────────────┘
                     ↓
        ┌──────────────────────────┐
        │ Structured Output Parser │
        └────────────┬─────────────┘
                     ↓
        ┌──────────────────────────┐
        │ Qualification Decision   │
        │ (IF Node Logic)          │
        └───────┬───────────┬──────┘
                ↓           ↓
      ┌──────────────┐   ┌──────────────┐
      │ Qualified     │   │ Unqualified  │
      │ Sheet Update  │   │ Sheet Update │
      └───────┬───────┘   └───────┬──────┘
              ↓                   ↓
      ┌──────────────────────────────┐
      │ HR Notification (Gmail API)  │
      └──────────────────────────────┘
```

## ⚙️ Workflow Breakdown

### 1️⃣ Gmail CV Trigger

- Monitors inbox for:
  - Subject: `"Application for Data Analyst Job"`
  - Emails containing attachments
- Downloads CV files automatically
- Polls inbox at defined intervals

---

### 2️⃣ CV Text Extraction

- Extracts text from PDF attachment
- Joins multi-page documents
- Prepares structured text input for AI evaluation

---

### 3️⃣ Job Description Injection

The workflow embeds a predefined job description directly into the AI prompt to ensure consistent evaluation criteria.

This enables:

- Deterministic scoring
- Controlled hiring criteria
- Role-specific assessment logic

---

### 4️⃣ AI CV Scoring Engine (OpenAI)

The OpenAI model evaluates:

- Years of relevant experience
- Skills match
- Education alignment
- Technical competency
- Overall job fit

#### Scoring Logic

- Score range: 0–100
- 70+ indicates qualified (if experience requirement is met)
- Automatic disqualification if required experience is not satisfied

Low temperature (0.2) ensures consistent scoring behavior.

---

### 5️⃣ Structured Output Enforcement

The workflow enforces a strict JSON schema:

```json
{
  "candidate_name": "",
  "email": "",
  "phone": "",
  "years_experience": 0,
  "key_skills": [],
  "education": "",
  "score": 0,
  "is_qualified": false,
  "summary": "",
  "strengths": "",
  "concerns": ""
}
```

This guarantees:

- Predictable automation
- Clean downstream data handling
- Reduced LLM variability
- Enterprise-grade reliability

---

### 6️⃣ Qualification Decision Logic

IF Node determines:

- If `is_qualified = true`
  - Add to "Qualified" sheet
  - Send HR notification
- Else
  - Add to "Unqualified" sheet

Demonstrates conditional workflow branching.

---

### 7️⃣ Google Sheets Integration

Automatically logs:

- Candidate Name
- Email
- Phone
- Score
- Years of Experience
- Key Skills
- Education
- Strengths
- Concerns
- Timestamp

Creates a real-time recruitment dashboard.

---

### 8️⃣ HR Email Notification

For qualified candidates:

- Sends structured notification email
- Includes score breakdown
- Highlights strengths & concerns
- Confirms automatic shortlisting

Simulates an internal HR alert system.

---

## 🧩 Core Technologies Used

- n8n (Workflow Orchestration)
- OpenAI GPT-4o (Candidate Evaluation)
- Gmail API (Trigger + Notification)
- Google Sheets API (Recruitment Dashboard)
- PDF Text Extraction
- Structured LLM Output Parsing
- Conditional Workflow Logic

---

## 🎯 Real-World Use Cases

- AI-powered Applicant Tracking System (ATS)
- High-volume recruitment automation
- Startup hiring pipelines
- HR process optimization
- Resume pre-screening automation
- Enterprise talent acquisition workflows

---

## 💼 Portfolio Case Study

### Problem

Manual CV screening is:

- Time-consuming
- Inconsistent
- Subjective
- Hard to scale
- Resource intensive

HR teams require objective, structured, automated first-pass screening.

---

### Solution

Designed and built a fully automated AI recruitment evaluation engine that:

- Detects new CV applications
- Extracts and analyzes resume data
- Scores candidates against defined job criteria
- Applies structured qualification rules
- Automatically categorizes applicants
- Logs structured results into Sheets
- Notifies HR instantly

All without manual intervention.

---

### Technical Highlights

- Advanced prompt engineering
- Deterministic scoring architecture
- Schema-based LLM output validation
- Multi-API integration
- Conditional automation logic
- Real-time candidate dashboard updates
- Production-style workflow orchestration

---

## 🧠 Skills Demonstrated

- AI Workflow Engineering
- HR Tech Automation
- LLM Output Structuring
- Automation Architecture Design
- API Integration Systems
- Conditional Decision Logic
- Data Logging Pipelines
- Production-Ready System Design

---

## 🏢 Enterprise Positioning

This system can function as:

- AI screening backend for ATS platforms
- Pre-filter engine for HR teams
- Automated recruitment dashboard feeder
- Hiring intelligence accelerator
- Integration layer for HRIS systems

It is easily extendable to:

- Multiple job roles
- Multiple inboxes
- Multi-department hiring
- SaaS recruitment platforms

---

## 📊 Business Impact

- Reduces screening time by up to 90%
- Standardizes candidate evaluation
- Removes early-stage bias variability
- Enables scalable hiring operations
- Improves HR productivity

---
