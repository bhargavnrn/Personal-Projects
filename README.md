# Personal-Projects
This is my personal repository to upload my personal projects
# Agentics AI – Workflow Automation System

Agentics AI is an AI-powered ticket management and workflow automation system designed to streamline ticket handling across multi-level agents and departments. This solution integrates with Git, Jira, Outlook (SMTP email), and supports optional Power BI dashboard refresh triggers.

## 📝 **Features**

- API endpoint to submit new tickets
- Ticket routed through Level 1 → Level 2 agents based on department
- Automatic Git commit to trigger workflows
- Jira story creation for each ticket
- Supervisor notification via Outlook email
- Placeholder for Power BI dashboard refresh integration
- Credentials loaded securely from `.env` file

## 🚀 **Tech Stack**

- Python
- FastAPI
- OpenAI Codex CLI (optional automation)
- Google ADK (optional ML integration)
- Jira Python API
- GitPython
- SMTPLib
- Power BI REST API (optional)

---

## 🔧 **Setup Instructions**

1. **Clone the repository:**

```bash
git clone https://github.com/bhargavnrn/Personal-Projects.git
cd Personal-Projects
