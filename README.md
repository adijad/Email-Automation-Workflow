# AI-Powered Email Outreach Automation (n8n + LLM)

This project is an end-to-end automation pipeline designed to streamline and scale personalized cold outreach. It leverages document parsing, workflow orchestration, and large language models to automatically generate tailored emails, attach relevant documents, and track outreach activity, all within a single unified system built on **n8n**.

---

## Overview

At a high level, this system takes raw inputs, a contact list and a resume and transforms them into structured, actionable outreach. Instead of manually drafting emails and tracking communication, the workflow automates the entire process while still preserving human control through draft-based email generation.

The pipeline is built with a strong focus on **scalability, personalization, and reliability**. Each contact is processed independently, ensuring that emails are customized rather than templated, and that the system can handle large batches without breaking.

---

## System Architecture

![Email Automation Workflow](./Email%20Automation%20Workflow.png)

The architecture is implemented as a multi-stage workflow in n8n. It begins with a form submission trigger, which accepts both a contacts document and a resume. These documents are processed in parallel, converted into structured JSON, and then merged into a unified data representation.

Once combined, the workflow iterates over each contact using a loop-based execution model. For every individual entry, an AI agent generates a personalized email based on the candidate’s background and the context of the contact. The resume is dynamically attached, and a draft email is created using the Gmail integration.

Finally, each outreach attempt is logged into Google Sheets, allowing for systematic tracking of sent emails and responses. A wait node is used to control execution pacing and prevent rate limiting.

---

## ⚙️ Workflow Details

The workflow starts with document ingestion, where both the contacts file and resume are extracted and parsed into structured formats. This ensures that downstream nodes operate on clean, normalized data rather than raw text.

The merging stage plays a critical role by combining multiple input branches into a single coherent structure. This allows the system to maintain context when generating emails, ensuring that both candidate information and contact details are available simultaneously.

The iteration layer is designed for scalability. By looping over each contact, the system avoids batch-level failures and enables independent processing. This is particularly important when dealing with large outreach campaigns.

At the core of the system is the AI agent, which generates email content under strict constraints. The emails are concise, personalized, and structured, typically following a three-part format: introduction, relevant experience, and intent. The output is enforced in a JSON format to ensure compatibility with downstream nodes.

The resume attachment step converts the uploaded document into a binary format that can be seamlessly attached to each generated email draft. This eliminates the need for manual file handling.

Email drafts are created rather than sent automatically, providing a safety layer that allows for manual review before outreach. This design choice balances automation with control.

Finally, the system logs each outreach event into Google Sheets, marking emails as sent and initializing response tracking fields. This creates a lightweight CRM-like layer for monitoring progress.

---

## Tech Stack

This project is built using a combination of workflow automation, AI, and cloud integrations:

- **n8n** for orchestration and workflow management  
- **LLM (AI Agent)** for personalized email generation  
- **Gmail API** for draft creation and email handling  
- **Google Sheets API** for tracking and logging  
- **PDF parsing nodes** for structured data extraction  

---

## Key Features

The system is designed with practical, production-oriented features:

- Fully automated outreach pipeline from input to tracking  
- AI-generated, personalized emails instead of static templates  
- Dynamic resume attachment for each contact  
- Loop-based processing for scalability  
- Draft-first approach to prevent accidental sends  
- Integrated tracking system using Google Sheets  

---

## Usage

To use this workflow, import it into n8n and configure the required credentials, including Gmail, Google Sheets, and your LLM provider. Once set up, provide a contacts PDF and resume through the form trigger.

The workflow will automatically process the inputs, generate personalized email drafts, attach the resume, and log each entry into your tracking sheet. You can then review and send the drafts as needed.

---

## Future Improvements

There are several natural extensions to this system that can further enhance its capabilities. These include automatic email sending after approval, LinkedIn-based enrichment for better personalization, follow-up email automation, response detection, and integration with a full CRM system.

---
