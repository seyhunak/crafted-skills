---
name: crafted-mcp
display_name: Crafted MCP Agents
description: "Dispatch tasks to Crafted's AI-powered AI agents via MCP. Use when the user needs banking, sales, marketing, real estate, HR, document processing, research, customer support, development, data analysis, or compliance workflows powered by AI agents."
---

## Overview

Crafted MCP Agents is a collection of AI-powered AI agents exposed via MCP (Model Context Protocol). Each agent is a self-contained AI flow specializing in a specific business domain — from banking compliance to sales automation to deep research.

This skill provides:
1. **MCP connection configuration** for connecting to the Crafted AI server
2. **Agent routing catalog** organized by domain
3. **Invocation patterns** for calling the right agent

## MCP Connection Configuration

Add this to your MCP client configuration (e.g., `.mcp.json`, Claude Desktop config, or Cursor MCP settings):

```json
{
  "mcpServers": {
    "lf-in_house": {
      "command": "uvx",
      "args": [
        "mcp-proxy",
        "--headers",
        "x-api-key",
        "CRAFTED_API_KEY",
        "http://lf.we-crafted.com:7860/api/v1/mcp/project/cee4876d-8279-4450-ad85-5a111cc4390a/streamable"
      ]
    }
  }
}
```

### Connection Architecture

| Component | Detail |
|-----------|--------|
| **Protocol** | MCP (Model Context Protocol) via Streamable HTTP |
| **Proxy** | `uvx mcp-proxy` (Python MCP-to-HTTP bridge) |
| **AI Server** | `lf.we-crafted.com:7860` |
| **Project ID** | `cee4876d-8279-4450-ad85-5a111cc4390a` |
| **Auth** | API key header (`x-api-key: CRAFTED_API_KEY`) |
| **Endpoint** | `/api/v1/mcp/project/{project_id}/streamable` |
| **Transport** | Streamable HTTP (AI v1.9+ native MCP server) |

### Prerequisites

1. Install `uvx` (Python package runner): `pip install uv`
2. Replace `CRAFTED_API_KEY` with your actual API key
3. The AI server must be accessible at `lf.we-crafted.com:7860`

### How It Works

1. **MCP Proxy** (`uvx mcp-proxy`) bridges local MCP stdio transport to the remote AI HTTP endpoint
2. **AI MCP Server** exposes all flows in the project as individual MCP tools
3. Each flow becomes a callable tool with the naming pattern: `lf_in_house__<flow_name>`
4. All tools accept `input_value` (string) as primary parameter — this maps to the AI flow's chat input

## Agent Catalog

### 🏦 Banking & Finance

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Credit Risk Analyst | `credit_risk_analyst_agent` | Evaluate loan applications, score creditworthiness, monitor portfolio risk |
| KYC/ODD/EDD Due Diligence | `kyc_odd_edd_due_diligence_agen` | KYC checks, customer due diligence, enhanced due diligence |
| Personalized Banking | `personalized_banking_experienc` | Customer behavior monitoring, product recommendations, retention campaigns |
| Customer Relationship Support | `customer_relationship_support_` | Handle customer interactions, churn risk detection, escalation |
| Insurance Underwriting | `insurance_underwriting` | Insurance risk assessment and underwriting decisions |
| Internal Auditor | `internal_auditor` | Process reviews, internal control effectiveness checks |
| Energy Trading Deal Processing | `energy_trading_deal_processing` | Process deal confirmations, extract structured data, credit checks |
| Trading Intelligence | `trading_intelligence` | Trading insights and market intelligence |
| Financial Market Analysis | `financial_market_analysis` | Company analysis, stock insights from latest news |
| Stock Market Analysis | `stock_market_analysis` | Real-time stock data retrieval for investors |
| SaaS Pricing Calculator | `saas_pricing_demo` | Calculate SaaS subscription pricing (costs, margin, subscribers) |

### 🏢 Sales & Lead Generation

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Sales Offer Generation | `sales_offer_generation` | Lead scoring, qualification, CRM integration |
| Real Estate Lead Qualification | `real_estate_lead_qualification` | Filter serious rental/sales inquiries (Dubai market) |
| Prospect Matcher | `prospect_matcher` | Email ↔ LinkedIn resolution, professional enrichment |
| LinkedIn Recruiter | `linkedin_recruiter` | LinkedIn-based recruiting outreach |
| Opportunity Discovery | `opportunity_discovery_for_ente` | Enterprise opportunity identification |
| Price Deal Finder | `price_deal_finder` | Compare prices across online retailers |
| Reddit Listener | `reddit_listener_agent` | Monitor Reddit for buying intent signals |
| Customer Segmentation | `customer_segmentation` | RFM analysis via Supabase/PostgreSQL |

### 📢 Marketing & Content

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Ad Copy | `ad_copy` | Generate advertising copy |
| Marketing Content Creation | `marketing_content_creation` | Create marketing materials |
| Newsletter Multi-Agent | `newsletter_multiagent` | Multi-agent newsletter generation |
| Landing Page Optimization | `landing_page_optimization` | Audit landing pages, extract competitor insights |
| Landing Page Analysis | `analyze_landing_page_and_get_o` | Diagnose sales leaks on landing pages |
| AB Test Results Analyzer | `ab_test_results_analyzer` | Analyze A/B test outcomes |
| AI Visibility Analytics | `ai_visibility_analytics_agent` | Track AI-powered visibility metrics |
| Voice of Customer Report | `voice_of_customer_report_gener` | Consolidate YouTube/Reddit feedback, sentiment analysis |

### 🏘️ Real Estate

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Real Estate Intelligence | `real_estate_intelligence_agent` | Real estate market analysis and intelligence |
| Real Estate Lead Qualification | `real_estate_lead_qualification` | Filter and qualify property inquiries |

### 👥 HR & Recruitment

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Resume Screening | `resume_screening_hiring_recomm` | Evaluate resumes against job requirements |
| AI Candidate Screening | `ai_powered_candidate_screening` | Multi-stage AI recruitment pipeline |
| Recruitment Agent | `recruitment_agent` | Automated recruitment bot |
| Resume Auditor | `resume_auditor` | Resume & cover letter generation/review |
| Job Seeker | `job_seeker` | Job search assistance |
| Onboarding Roadmap | `onboarding_roadmap_agent` | Build onboarding plans (30-day roadmaps) |
| Training Coach | `training_couch` | Employee training and coaching |

### 📄 Document Processing & RAG

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| AWS Labs Document QA | `aws_labs_document_qa` | PDF reading + LLM Q&A for documents |
| Chat with Invoice PDF | `chat_with_invoice_pdf` | AI accountant for invoice analysis |
| Document Classification | `document_classification` | Classify documents by type |
| Docling AI Agent | `docling_ai_agent` | Turn messy documents into structured data |
| Document Translation | `document_translation_system` | Translate documents chunk by chunk |
| Vector Store RAG | `vector_store_rag` | RAG with vector database |
| Hybrid Search RAG | `hybrid_search_rag` | Hybrid keyword + semantic search |
| RAG Article from Web | `rag_article_in_web_with_agent` | Create RAG chunks from URL content |
| Local RAG (Ollama + ChromaDB) | `local_rag_ollama_chromadb` | Local RAG pipeline |
| RAG Ingestion from Google Drive | `rag_ingestion_from_google_driv` | Ingest Google Drive docs into RAG |
| Ingestion Router | `ingestion_router` | Route documents to appropriate ingestion pipeline |

### 🔬 Research & Analysis

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Deep Research | `deep_research` | In-depth research on any topic |
| Research News Agent | `research_news_agent` | News research and aggregation |
| Smart Market Researcher | `smart_market_researcher` | Market research and competitive intelligence |
| Discovery | `discovery` | Exploration and discovery tasks |
| Industry Classification | `industry_classification_regula` | Classify industries, regulatory analysis |

### 🛡️ Compliance & Risk

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| AI Contract Risk Scanner | `ai_contract_risk_scanner` | Scan contracts for risk clauses |
| Vendor Assessment | `vendor_assessment_agent` | Evaluate vendor risk and suitability |
| Red Teaming | `red_teaming` | Security red team exercises |
| Red Teamer | `red_teamer` | Adversarial testing |

### 💻 Development & DevOps

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Chat with Codebase | `chat_with_codebase` | Code repository Q&A |
| Code Drift | `code_drift` | Generate commit messages |
| Xcodebuild | `xcodebuild` | iOS/macOS build, run, debug via Xcode |
| Firebase MCP Server | `firebase_mcp_server` | Firebase operations (auth, DB, functions) |
| GitHub MCP Server | `github_mcp_server` | GitHub operations (repos, PRs, issues) |
| TestSprite (QA) | `testsprite` | QA testing agent |
| Data Pipeline | `data_pipeline` | Natural language → data transformations |
| NVIDIA RTX Remix | `nvidia_rtx_remix` | NVIDIA RTX Remix Toolkit API integration |

### 🎯 Product & Project Management

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Product Owner | `product_owner` | Senior PO & delivery tasks |
| Change Manager | `change_manager` | Change requests in Asana |
| Feature Prioritization | `feature_prioritization_scorer` | Score and prioritize features |
| Prioritization Agent | `prioritization_agent` | General task/business prioritization |
| KPI Report Generator | `kpi_report_generator` | Generate KPI reports |
| Intelligent Organization | `intelligent_organization` | Organizational intelligence tasks |

### 📅 Productivity & Calendar

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Google Calendar Organizer | `google_calendar_organizer` | Calendar management |
| Daily Calendar Brief | `daily_calendar_brief` | Morning calendar summary |
| Pre-Meeting Brief | `pre_meeting_brief_automation_t` | Generate pre-meeting briefings |
| Email Calendar Integration | `email_calendar_integration` | Email + calendar coordination |
| Conference Preparation | `conference_preparation` | CRM + email + workspace prep for conferences |

### 🎨 Creative & Visualization

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Generate Images | `generate_images` | AI image generation |
| Markdown Converter (Mindmap) | `markdown_converter` | Convert markdown to interactive mind maps |
| JSON Render | `json_render` | Generate dashboards/widgets from prompts |
| Interactive Data Dashboards | `interactive_data_dashboards` | Natural language → SQL → charts |

### 🎙️ Voice & Communication

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Voice | `voice` | Voice-based conversation |
| Voice to Structured Text | `voice_to_structured_text` | Convert voice to structured text |
| CX Agent | `cx_agent` | Conversational customer experience |
| Customer Support Agent | `customer_support_agent` | Product docs search, order status, escalation |
| Memory Chatbot | `memory_chatbot` | Context-preserving conversation |

### 🚢 Industry-Specific

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| Marinesia Vessel Tracking | `marinesia_vessel_tracking` | Ship/port tracking for maritime |
| Collect (Product Scraping) | `collect` | Collect products from web |
| JotForm Submission | `jotform_submission` | Process JotForm lead submissions |

### 🔧 Utility

| Agent | Tool Name | Use When |
|-------|-----------|----------|
| CUGA (Context7 MCP) | `cuga` | Resolve library docs, fetch authoritative sources |
| Ticket Analysis & Classification | `ticket_analysis_classification` | Classify tickets by severity and sentiment |
| Call Classification Analytics | `call_classification_analytics` | Analyze and classify calls |
| UCP | `ucp` | Unified communication platform tasks |

## Usage

### Basic Invocation

All agents follow the same pattern:

```
Tool: lf_in_house__<agent_name>
Input: { "input_value": "your message or query here" }
```

### Special Parameters

Some agents accept additional parameters:

| Agent | Extra Parameters |
|-------|-----------------|
| `sales_offer_generation` | `data` (HTTP payload string), `endpoint` (URL) |
| `aws_labs_document_qa` | `should_store_message` (boolean) |

### Agent Selection Rules

1. **Match by domain first** — banking tasks → banking agents, hiring → HR agents
2. **Prefer specific over generic** — e.g., `energy_trading_deal_processing` over `financial_market_analysis` for trade confirmations
3. **Chain for compound tasks** — research → content creation, screening → onboarding
4. **When ambiguous** — ask which domain applies

### Example: Processing an Energy Trade

```
Input: "DEAL CONFIRMATION — REF: ETC-2025-0118, Seller: Gulf Stream Energy DMCC,
        Buyer: Horizon Power Trading FZE, Commodity: Natural Gas, Volume: 50,000 MMBtu..."

Agent: energy_trading_deal_processing
Result: Extracted structured data, validated contract value, ran credit check → Approved
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Connection refused | Verify AI server is running at `lf.we-crafted.com:7860` |
| Authentication error | Check API key is valid and correctly set |
| Empty response | Provide more specific input; some agents need detailed context |
| Timeout | `deep_research` and `conference_preparation` take longer — be patient |
| Tool not found | MCP proxy may have lost connection; restart the proxy |
