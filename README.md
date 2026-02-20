# AI-Powered Automated CV Screening & Candidate Shortlisting with n8n

![AI-Powered CV Screening and Candidate Shortlisting](https://github.com/user-attachments/assets/dc48e631-6f90-45f3-894b-6ee2cf003e68)


🤖 **Fully automated resume screening pipeline** that reads CVs from Gmail, extracts content, evaluates candidates using OpenAI GPT-4o, scores them (0–100), shortlists qualified applicants (≥70 + experience check), stores everything in Google Sheets, and instantly notifies your HR team via email.

Built with **n8n** – the open-source workflow automation tool.

## ✨ Features

- Gmail trigger → only processes emails with subject `"Application for Data Analyst Job"` + attachment
- Extracts text from attached PDF resumes (first attachment)
- Uses **GPT-4o** to analyze CV against job description
- Strict experience gate: disqualifies candidates below required years (even if score ≥70)
- Structured JSON output: name, email, phone, years experience, skills, education, score, strengths, concerns, summary
- Qualified candidates (score ≥70 **and** experience ok) → Google Sheet + HR email notification
- All candidates (qualified + unqualified) → logged in separate Google Sheets tabs
- Low temperature (0.2) for consistent, objective scoring

## 🏗️ Workflow Overview
![Workflow overview](https://github.com/user-attachments/assets/a29824f4-7d1b-4942-bb8e-fa3bfeecefe0)


## 🚀 Technologies / Services

- **n8n** (self-hosted or cloud)
- **Gmail** (trigger + sending notifications)
- **OpenAI** (gpt-4o model)
- **Google Sheets** (two tabs: Qualified + Unqualified)
- **Extract From File** node (PDF text extraction)

## 📋 Prerequisites

1. n8n instance (latest version recommended)
2. Gmail OAuth2 credentials (for trigger & send)
3. OpenAI API key
4. Google Sheets OAuth2 credentials
5. Google Sheet with two tabs:
   - "Qualified" (gid=0)
   - "Unqualified" (gid=588558509)
   → Share the sheet link with your service account / OAuth user

## 🛠️ How to Install / Use

1. Clone or download this repository
2. Go to n8n → **Import from File** (or **Import from URL** if you host the .json file)
3. Upload the `.json` workflow file
4. Connect your credentials:
   - Gmail OAuth2
   - OpenAI API
   - Google Sheets OAuth2
5. Update the **job_description** value in the "Workflow Configuration" node
6. (Optional) Change the HR email in "Send HR Notification" node
7. Activate the workflow

## ⚙️ Customization Ideas

- Add more job descriptions and use a Switch node
- Filter attachments by filename (e.g. contains "CV" or ".pdf")
- Add rejection email for unqualified candidates
- Connect to ATS (Greenhouse, Lever, Workable, etc.)
- Use a cheaper/faster model (gpt-4o-mini, Claude 3.5 Sonnet via OpenRouter, etc.)
- Add GitHub profile analysis for tech roles

## 📄 License

MIT – feel free to use, modify, and share.

## 🙌 Show your support

If this saves you hours of manual CV screening → give the repo a ⭐!

Questions, improvements, or forks → open an issue or PR.

Happy automating! 🚀
