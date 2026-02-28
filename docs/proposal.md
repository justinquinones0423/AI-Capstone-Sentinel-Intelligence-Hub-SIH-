# Security Alert Triage Bot

## Team Members

| Name | Role/Component | GitHub Username |
|------|---------------|-----------------|
| Justin Quinones | Ingestion | @justinquinones0423 |
| Alexander Lustig | Analysis | @AlexanderLustig |
| Ujjwal Singh | Action | @ujjwalsingh7 |
| Abdoul Sawadogo | Monitoring | @abdoulsaw5 |

## Problem Statement

Security Operations Center (SOC) analysts are currently overwhelmed by a massive volume of security alerts, many of which are low-priority or false positives. This "alert fatigue" leads to critical threats being missed or delayed in response. By automating the initial triage, analysis, and prioritization, this project ensures that human analysts only spend time on high-impact, verified incidents.

## Target Users
The primary users are SOC Analysts and Security Managers at mid-to-large sized organizations who handle hundreds of daily alerts and need an automated system to prioritize critical threats and reduce manual ticket creation.

## Architecture

![Architecture Diagram](docs/AI%20Security%20Alert%20Triage%20Bot%20-%20System%20Architecture.png)

## Component Breakdown
### Component 1: Ingestion (Owner: Justin Quinones)
- **Description:** An n8n workflow that accepts incoming security alerts via webhooks from various formats and normalizes them into a common schema.
- **Tools:** n8n, Airtable.
- **Input:** Raw JSON/Webhook data from simulated security tools (Firewalls, EDR).
- **Output:** Standardized, normalized alert records stored in Airtable.
- **Standalone demo:** A successful curl command sending a raw JSON payload that appears instantly as a formatted row in Airtable.

### Component 2: Analysis (Owner: Alexander Lustig)
- **Description:** A multi-agent AI system (analyst, researcher, recommender) that performs deep reasoning on the alert to determine its validity.
- **Tools:** CrewAI/LangGraph, Groq.
- **Input:** Normalized alert data from Airtable.
- **Output:** A reasoning trace and a final triage recommendation (True/False Positive).
- **Standalone demo:** A Python script taking a static JSON alert and outputting a detailed "Analyst Reasoning" report.

### Component 3: Action (Owner: Ujjwal Singh)
- **Description:** An n8n workflow that creates tickets in external systems and follows configurable escalation rules based on AI findings.
- **Tools:** n8n, Linear/GitHub Issues.
- **Input:** Triage recommendation and summary from the Analysis component.
- **Output:** Automatically generated tickets or closed alerts with resolution notes.
- **Standalone demo:** Triggering the workflow to automatically create a GitHub Issue based on a "High" severity input.

### Component 4: Monitoring (Owner: Abdoul Sawadogo)
- **Description:** A visual dashboard that displays triage volume, severity distribution, and response time metrics.
- **Tools:** Streamlit, Airtable.
- **Input:** All processed records and timestamps from Airtable.
- **Output:** Real-time charts and a "Command Center" view for SOC managers.
- **Standalone demo:** A web-accessible Streamlit page that updates dynamically when new test data is added to Airtable.

## Data Sources

- **Primary data:** Simulated security alerts (e.g., Brute force attempts, SQL injection, unauthorized logins).
- **Sample data:** A custom JSON dataset of 50-100 "mock alerts" reflecting different severity levels and attack types.
- **Data format:** JSON (for webhooks) and Airtable Records.

## AI Capabilities

| Capability | Purpose | Model/API |
|-----------|---------|-----------|
| Multi-Agent Reasoning | To research threats and recommend triage steps | CrewAI / Groq LLaMA 3 |
| Summarization | Turning technical logs into concise incident summaries | Groq LLaMA 3


## Success Criteria
1. System correctly identifies and normalizes 90% of incoming test alert formats.
2. The AI multi-agent system provides a reasoning trace for every processed alert.
3. High-priority alerts result in an automatically created ticket in GitHub Issues within 60 seconds.
4. The Streamlit dashboard accurately displays metrics for at least 50 test incidents.
5. All 4 components successfully exchange data through the central Airtable "Source of Truth."

## Timeline

| Week | Milestone |
|------|-----------|
| 3 (Now) | Project proposal + architecture diagram + GitHub repo |
| 4-6 | Build individual components, test with sample data |
| 7-9 | Add LLM/agent capabilities, refine AI processing |
| 10-12 | Full system integration and error handling (End-to-end testing)|
| 13-14 | Polish UI, finalize documentation, and record demo |
| 15 | Final presentation |


Our group focuses on creating a highly modular architecture where each member has a distinct,
standalone piece of the puzzle that communicates through a central Airtable "Source of Truth".
By choosing the Security Alert Triage Bot, we are able to leverage our collective interests in cybersecurity and automation, while ensuring the lead engineer has enough room to implement complex multi-agent logic.

