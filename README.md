🗺️ Google Maps AI Agent

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![n8n](https://img.shields.io/badge/Workflow-n8n-orange)](https://n8n.io/)
[![OpenAI](https://img.shields.io/badge/AI-GPT--4o-blue)](https://openai.com/)
[![AI Powered](https://img.shields.io/badge/AI-Conversational-brightgreen)](https://github.com)

> 💥 **Developed by xCodeWraith**


> **A conversational AI agent that extracts, enriches, and organizes business leads from Google Maps using natural language.**

Simply chat with the AI: *"Find 100 dental clinics in Los Angeles"* and watch it automatically scrape, enrich, and organize the data into Google Sheets.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [How It Works](#-how-it-works)
- [Tech Stack](#-tech-stack)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage Examples](#-usage-examples)
- [Data Fields](#-data-fields)
- [Troubleshooting](#-troubleshooting)
- [License](#-license)

---

## 🎯 Overview

**Google Maps AI Agent** is an intelligent conversational system that transforms Google Maps into a powerful B2B lead generation tool. Instead of manually searching and copying business data, simply chat with an AI agent that understands your requirements and automates the entire process.

### What Makes This System Special?

- 🤖 **Natural Language Interface** - Chat naturally as if speaking to a human assistant
- 🧠 **AI-Powered Understanding** - GPT-4o intelligently interprets your requests
- 🔄 **Automatic Enrichment** - Automatically finds emails and company backgrounds
- 📊 **Smart Organization** - Structures data perfectly in Google Sheets
- ⚡ **Real-Time Processing** - Watch leads populate as you chat

### Who Is This For?

| Target Audience | Use Case |
|-----------------|----------|
| 💼 **Sales Teams** | Targeted lead lists by location and niche |
| 📞 **Cold Callers** | Get phone numbers and business info instantly |
| 📧 **Email Marketers** | Contact info with email enrichment |
| 🏢 **B2B Agencies** | Local business research for clients |
| 🚀 **Entrepreneurs** | Find potential clients or partners |

---

## ✨ Key Features

### 🗣️ Conversational Interface
- Natural language input: *"Find 50 restaurants in NYC"*
- No complex forms or parameters
- AI understands context and intent
- Multi-turn conversations

### 🔍 Intelligent Google Maps Scraping
- Search via Serper.dev Google Maps API
- Automatically handles pagination
- Extracts comprehensive business data
- Geo-targeting with coordinates

### 📧 Automated Email Enrichment
- Perplexity AI finds company emails
- Automatic web scraping from websites
- Background research for every business
- Real-time updates to Google Sheets

### 🔄 Two-Stage Workflow


```

┌──────────────────────────────────────────────────────────┐
│                   STAGE 1: DATA COLLECTION               │
├──────────────────────────────────────────────────────────┤
│  Chat Trigger → AI Agent → Serper API → Sub-Workflow     │
│                                           ↓              │
│                                  Google Sheets Save      │
└──────────────────────────────────────────────────────────┘
↓
┌──────────────────────────────────────────────────────────┐
│                   STAGE 2: ENRICHMENT                    │
├──────────────────────────────────────────────────────────┤
│  Sheets Trigger → Perplexity AI → Email & Background     │
│                                           ↓              │
│                                  Sheets Update           │
└──────────────────────────────────────────────────────────┘

```

---

## 🔄 How It Works

### User Experience


```

You: "Extract info for 100 dental clinics in Los Angeles"

AI Agent: "I'll search for dental clinics in Los Angeles. Starting now..."
[Google Maps search]
[Finds 100+ results across multiple pages]
[Automatically saves to Google Sheets]

AI Agent: "✅ Found and saved 97 dental clinics to your sheet!"

[Background process starts automatically]
[Enriches each lead with email and background]
[Updates the sheet with enriched data]

```

---

## 🛠️ Tech Stack

| Category | Technology | Purpose |
|----------|------------|---------|
| **Automation** | n8n | Workflow orchestration |
| **AI Agent** | OpenAI GPT-4o | Natural language understanding & task execution |
| **AI Memory** | Buffer Window | Conversation context retention |
| **Map Search** | Serper.dev | Google Maps API for business data |
| **Enrichment** | Perplexity AI (Sonar) | Email discovery & company research |
| **Storage** | Google Sheets | Lead database |

---

## 📦 Requirements

### Required Accounts & API Keys

| Service | Required? | Purpose | Cost |
|---------|-----------|---------|------|
| **n8n** | ✅ Yes | Run workflows | Free (self-hosted) or $20/mo |
| **OpenAI** | ✅ Yes | GPT-4o AI agent | ~$0.01-0.03 per request |
| **Serper.dev** | ✅ Yes | Google Maps search | $50/mo for 5,000 searches |
| **Perplexity AI** | ✅ Yes | Email enrichment | $20/mo or pay-per-use |
| **Google Account** | ✅ Yes | Google Sheets storage | Free |

---

## 🚀 Installation

> ⚠️ **IMPORTANT:** This system consists of 2 separate workflows. Both must be imported separately and linked together!

### 📦 Workflow Files

| File | Type | Description |
|------|------|-------------|
| `Google map ai agent.json` | **Main Workflow** | Chat interface and AI agent |
| `Gooogle map lead ai agent.json` | **Sub-Workflow** | Data saving and UUID generation |

---

### Step 1: FIRST Import the Sub-Workflow

> 🔴 **ORDER MATTERS!** The sub-workflow MUST be imported first!

1. Open n8n
2. Click **"Workflows"** → **"Import from File"**
3. Select `Gooogle map lead ai agent.json`
4. Click **"Import"**
5. ✅ Once imported, **note down the workflow ID:**
   - Visible in URL: `https://your-n8n.com/workflow/WORKFLOW_ID`

---

### Step 2: Import the Main Workflow

1. Click **"Workflows"** → **"Import from File"**
2. Select `Google map ai agent.json`
3. Click **"Import"**

---

### Step 3: Link the Two Workflows

> 🔗 The main workflow must be linked to call the sub-workflow!

1. Open the main workflow
2. Find the **"Call n8n Workflow Tool"** node
3. Click on the node
4. In the **"Workflow"** field:
   - Select **"💥 xCodeWraith - Google Maps Lead Sub-Workflow"** from the dropdown

---

### Step 4: Create Google Sheet

1. Go to https://sheets.google.com/
2. Create a new spreadsheet named: **"Leads Google map ai agent"**
3. Create headers in row 1:


```

UUID | Name | Address | Number | Website | Rating | Opening Hours | Email | Background

```

---

### Step 5: Update Google Sheets Nodes

Update Google Sheets nodes **in both workflows**:

**In Main Workflow:**
- `Google Sheets Trigger` node → Select your Spreadsheet ID
- `Google Sheets` (update) node → Select your Spreadsheet ID

**In Sub-Workflow:**
- `Append row in sheet` node → Select your Spreadsheet ID

---

### Step 6: Activate Workflows

1. Open the **Main workflow** → Toggle **"Active"** (green)
2. The **Sub-workflow** can remain inactive (it is called automatically by the main one)
3. Click the **"When chat message received"** node in the Main workflow
4. Copy the **"Production URL"**
5. Open this URL in a browser to access the chat interface!

---

## ⚙️ Configuration

### 1. OpenAI API Key

**Node:** "OpenAI Chat Model"

1. Get API key from https://platform.openai.com/api-keys
2. In n8n: **Settings** → **Credentials**
3. Add **"OpenAi account"** credential
4. Paste your API key

---

### 2. Serper.dev API Key

**Node:** "Map Search Tool"

1. Sign up at https://serper.dev/
2. Get API key from dashboard
3. Find the **Headers** section in the node
4. Update `X-API-KEY` value with your key

---

### 3. Perplexity API Key

**Node:** "Message a model1"

1. Get API key from https://www.perplexity.ai/settings/api
2. In n8n: **Settings** → **Credentials**
3. Add **"Perplexity account"** credential

---

### 4. Google Sheets OAuth

1. In n8n: **Settings** → **Credentials**
2. Add **"Google Sheets OAuth2 API"**
3. Follow the OAuth flow

---

## 📖 Usage Examples

### Example 1: Simple Search


```

You: "Find 50 coffee shops in Seattle"

AI: ✅ Found and saved 47 coffee shops!

```

### Example 2: Specific Niche


```

You: "Extract info for 100 dental clinics in Los Angeles"

AI: Searching for dental clinics in Los Angeles...
100 results = 5 pages to scan
✅ 97 dental clinics saved!

```

---

## 📊 Data Fields

| Field | Description | Source |
|-------|-------------|--------|
| **UUID** | Unique identifier | Auto-generated |
| **Name** | Business name | Google Maps |
| **Address** | Full address | Google Maps |
| **Number** | Phone number | Google Maps |
| **Website** | Company website | Google Maps |
| **Rating** | Google rating | Google Maps |
| **Opening Hours** | Operating hours | Google Maps |
| **Email** | Contact email | Perplexity AI |
| **Background** | Company description | Perplexity AI |

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Chat interface not loading | Verify Main workflow is **Active** |
| No results from map search | Check Serper.dev API key |
| Data not saving to Sheets | Verify Google Sheets credentials |
| Sub-workflow not running | Check workflow connection link |

---

## 📈 Performance Metrics

| Metric | Value |
|--------|-------|
| **Search Speed** | 20 results per page in 2 seconds |
| **Scraping** | ~100 leads in 1 minute |
| **Enrichment** | ~60 leads in 5-10 minutes |
| **Accuracy** | 90%+ data accuracy |
| **Daily Capacity** | 5,000-10,000 leads |

---

## 📄 License

This project is licensed under the **MIT License**.

✅ Commercial use allowed  
✅ Modification allowed  
✅ Distribution allowed  
✅ Private use allowed  
⚠️ No warranty or liability

---

**💥 Made with ❤️ by xCodeWraith**

⭐ Star this repo if it helps you generate leads!

---

**Ready to generate thousands of leads?** Start chatting with your AI agent now! 🗺️

```
