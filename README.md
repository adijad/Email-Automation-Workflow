# AI-Powered Email Outreach Automation (n8n + FastAPI + LLM)

An end-to-end automation pipeline that extracts contact + resume data, generates personalized cold emails using an AI agent, and logs outreach activity — all orchestrated via **n8n**.

---

## Overview

This project automates the entire cold outreach workflow:

1. Extracts structured data from uploaded documents (contacts + resume)
2. Merges and processes inputs
3. Uses an AI agent to generate personalized emails
4. Attaches resume automatically
5.  Creates email drafts
6.  Logs outreach status into Google Sheets

---

## System Architecture

![Email Automation Workflow](./Email%20Automation%20Workflow.png)

> Full workflow implemented in n8n showing document ingestion, AI email generation, and outreach logging pipeline.

---

## Workflow Breakdown

### Input Layer
- **Trigger:** `On form submission`
- Accepts:
  - Contact file (PDF)
  - Resume (PDF)

---

### Data Extraction
- **Extract contacts from PDF**
- **Extract resume from PDF**
- Converts both into structured JSON using parsing nodes

---

### Data Processing
- **Merge Node (cross-branch):**
  - Combines contact + resume data
- **Combine Inputs Node:**
  - Normalizes into a single structured object

---

### Iteration Engine
- **Loop Over Items**
  - Processes each contact independently
  - Ensures scalable outreach

---

### I Email Generation
- Uses an **AI Agent node**
- Generates:
  - `subject`
  - `body`
- Constraints:
  - ≤ 200 words
  - Personalized
  - Structured (Intro → Experience → Intent)
  - JSON output format

---

### Resume Attachment
- Converts resume into binary
- Attaches it dynamically to each email draft

---

### Email Draft Creation
- Uses Gmail node:
  - Creates draft emails (not sent automatically)
  - Ensures manual review capability

---

### Tracking & Logging
- Appends outreach data to Google Sheets:
  - Name
  - Email
  - Company
  - `mailed = YES`
  - `response_received = NO`

---
