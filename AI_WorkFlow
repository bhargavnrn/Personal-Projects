from fastapi import FastAPI
from pydantic import BaseModel
from jira import JIRA
import smtplib
from email.mime.text import MIMEText
from git import Repo

app = FastAPI()

# Ticket schema
class Ticket(BaseModel):
    title: str
    description: str
    department: str  # Development, Finance, Resource Management, IT

# Jira config
jira_server = ""
jira_username = ""
jira_token = ""
jira_project_key = ""

jira_client = JIRA(server=jira_server, basic_auth=(jira_username, jira_token))

# Email config
smtp_server = ""
smtp_port = 587
smtp_user = ""
smtp_password = ""

supervisor_email = ""

# Submit ticket endpoint
@app.post("/submit_ticket/")
def submit_ticket(ticket: Ticket):
    # Step 1: First agent scans ticket
    print(f"Ticket scanned by Level 1 Agent: {ticket.title}")

    # Step 2: Determine which Level 2 agent handles it
    agent_map = {
        "Development": "Agent 1",
        "Finance": "Agent 2",
        "Resource Management": "Agent 3",
        "IT": "Agent 4"
    }
    assigned_agent = agent_map.get(ticket.department, "Unknown")
    print(f"Ticket assigned to {assigned_agent}")

    # Step 3: Trigger Git workflow (simulated git commit)
    repo = Repo("/path/to/your/repo")
    repo.git.add(update=True)
    repo.index.commit(f"Trigger workflow for {ticket.department} ticket: {ticket.title}")
    print(f"Git commit triggered for {ticket.department}")

    # Step 4: Create Jira story
    jira_issue = jira_client.create_issue(
        project=jira_project_key,
        summary=ticket.title,
        description=ticket.description,
        issuetype={'name': 'Story'}
    )
    print(f"Jira issue {jira_issue.key} created")

    # Step 5: Send email notification
    msg = MIMEText(f"A new Jira story {jira_issue.key} has been created for {ticket.department}.")
    msg['Subject'] = f"Ticket Assigned: {ticket.title}"
    msg['From'] = smtp_user
    msg['To'] = supervisor_email

    with smtplib.SMTP(smtp_server, smtp_port) as server:
        server.starttls()
        server.login(smtp_user, smtp_password)
        server.sendmail(smtp_user, supervisor_email, msg.as_string())
        print("Notification email sent to supervisor.")

    # Step 6: Placeholder for Power BI refresh (replace with actual API call)
    print("Power BI dashboard refresh triggered (placeholder)")

    return {
        "status": "Ticket processed",
        "assigned_agent": assigned_agent,
        "jira_issue": jira_issue.key
    }
