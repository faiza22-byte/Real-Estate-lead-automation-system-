Demo video : https://www.linkedin.com/feed/update/urn:li:activity:7477716328699609088/
Here is a clean, professional `README.md` tailored for this workflow. It is structured specifically for a GitHub repository or portfolio showcase, highlighting the architecture, features, and an easy setup guide.

---

# Real Estate AI Lead Automation System

An enterprise-grade, event-driven automation workflow built in **n8n** that orchestrates lead intake, conversational AI qualification, automated CRM indexing, and intelligent scheduling.

This system bridges frontend web forms with voice-based Large Language Models (LLMs) to engage, qualify, and convert real estate leads asynchronously.

---

## 🚀 Features & Architecture

The workflow splits into two primary automated funnels:

### 1. Lead Intake & Initial Engagement

* **Instant Capture:** Ingests raw prospect criteria via an n8n web form or webhook endpoint.
* **Contextual Copie Generation:** Leverages **OpenAI (GPT-4o-mini)** to dynamically draft a responsive, luxury-themed HTML marketing email personalized with the lead's parameters.
* **CRM Synchronization:** Records the prospect into **Airtable** using conditional dynamic upsert keys to prevent duplicate records.
* **Dynamic Voice Bridging:** Dispatches a personalized outreach email containing an encrypted, unique link to a conversational voice consultant (**Vapi**).

### 2. Conversational AI Qualification & Closed-Loop Booking

* **Web-Hook Payload Parsing:** Processes the real-time transcript summary execution webhook once the lead concludes their call with the AI Voice Consultant.
* **Asynchronous LLM Extraction:** Evaluates call semantics using an OpenAI processing node to categorize buyer/seller intent, extract hard budgets, assess location preferences, and compute an immediate **Lead Quality Score** (e.g., *Hot* vs. *Warm*).
* **CRM State Updates:** Patches the historical Airtable lead record with the extracted structured JSON metrics.
* **Intelligent Routing:** If the prospect is flagged as *Interested*, the system automatically fires a high-conversion transactional email containing a **Cal.com** scheduling link pre-seeded with their unique CRM record metadata.

---

## 🛠️ System Tech Stack

* **Workflow Orchestration:** `n8n (v2 Architecture)`
* **Generative Intelligence:** `OpenAI API (GPT-4o-mini)`
* **Voice Agent Infrastructure:** `Vapi API`
* **Data Management / CRM:** `Airtable API`
* **Communication Engine:** `Gmail OAuth2 Secure Service`
* **Scheduling Gateway:** `Cal.com`

---

## 📋 Prerequisites & Environment Variables

To execute this workflow, ensure your environment configurations include the following platform credentials:

| Provider | Credential Type Required | Usage |
| --- | --- | --- |
| **n8n** | Self-hosted or Cloud instance | Runs the underlying JSON engine |
| **OpenAI** | `openAiApi` Personal Token | Generates copy drafts and handles semantic analysis |
| **Airtable** | `airtableTokenApi` (Personal Access Token) | Syncs client profile properties |
| **Google** | `gmailOAuth2` Client Authorization | Handles secure transactional mail dispatches |
| **Vapi** | Public Key / Webhook Authentication | Triggers outbound conversational audio streams |

---

## 🔧 Installation & Deployment Guide

1. **Clone the Workflow Asset:**
Download the provided `workflow.json` asset file locally from this repository.
2. **Import into n8n:**
* Open your local or production n8n dashboard.
* Navigate to **Workflows** -> **Add Workflow** (or select an empty canvas).
* Click the top-right menu icon and choose **Import from File**. Select your sanitized `workflow.json`.


3. **Configure the Environment Configurations Node:**
Locate the two `Config` nodes inside the visual canvas and populate your deployment parameters:
* `n8nBaseUrl`: Your public application endpoint or development ngrok tunnel domain.
* `vapiAssistantId` & `vapiPublicKey`: Your unique conversational bot identifiers.
* `calBookingLink`: Your targeted corporate calendar slug.


4. **Link Platform Credentials:**
Open the **OpenAI**, **Airtable**, and **Gmail** nodes individually and select your active credential profiles from the dropdown menus.
5. **Expose Production Webhooks:**
Toggle the workflow status from **Inactive** to **Active** to publish your webhook listener routes to live production.

---

## 🔒 Security Disclaimer

> [!IMPORTANT]
> This repository contains a fully sanitized configuration file. Production access strings, specific database schemas, proprietary ngrok subdomains, and credential identifiers have been substituted with generic `YOUR_PLACEHOLDER` configurations to adhere to open-source security best practices. Always use n8n environment variable injection or credential stores for production keys.
