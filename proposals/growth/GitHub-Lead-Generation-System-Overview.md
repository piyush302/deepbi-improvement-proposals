# GitHub Lead Generation System for Deep.BI

## Executive Summary

This document outlines an automated lead generation system that identifies potential customers from the Apache Druid GitHub repository community. The system extracts, enriches, and scores leads to help Deep.BI's sales team prioritize outreach to the most promising prospects.

---

## System Overview

```mermaid
flowchart TB
    subgraph Input["📥 Data Sources"]
        GH[("🐙 GitHub API<br/>Apache Druid Repo")]
        LI[("💼 LinkedIn")]
        TW[("🐦 Twitter/X")]
        CO[("🏢 Company Data<br/>Clearbit/Crunchbase")]
    end

    subgraph Process["⚙️ n8n Workflow Engine"]
        direction TB
        COLLECT["1️⃣ Collect GitHub Users<br/>Stargazers • Watchers • Issue Creators"]
        DELTA["2️⃣ Delta Detection<br/>Identify New Leads"]
        ENRICH["3️⃣ Profile Enrichment<br/>Social • LinkedIn • Company"]
        ANALYZE["4️⃣ Keyword Analysis<br/>druid • flink • starrocks"]
        SCORE["5️⃣ Lead Scoring<br/>Composite Score 0-100"]
        RECOMMEND["6️⃣ Outreach Recommendations<br/>Channel • Talking Points • Urgency"]
    end

    subgraph Output["📤 Outputs"]
        DB[("📊 Lead Database<br/>Google Sheets/Airtable")]
        REPORT["📈 Summary Reports"]
        ALERTS["🔔 Notifications"]
    end

    GH --> COLLECT
    COLLECT --> DELTA
    DELTA --> ENRICH
    LI --> ENRICH
    TW --> ENRICH
    CO --> ENRICH
    ENRICH --> ANALYZE
    ANALYZE --> SCORE
    SCORE --> RECOMMEND
    RECOMMEND --> DB
    RECOMMEND --> REPORT
    RECOMMEND --> ALERTS
```

---

## User Journey: From GitHub Activity to Qualified Lead

### Visual Flow

```mermaid
flowchart TD
    subgraph PHASE1["🎯 PHASE 1: GitHub Activity"]
        direction LR
        A1["⭐ Stars Repo"]
        A2["👁️ Watches Repo"]
        A3["🐛 Creates Issue"]
    end

    subgraph PHASE2["🔄 PHASE 2: Data Collection"]
        direction LR
        B1["📥 Extract Profile"]
        B2["🆕 Detect if New"]
    end

    subgraph PHASE3["🔍 PHASE 3: Enrichment"]
        direction LR
        C1["💼 Find LinkedIn"]
        C2["🏢 Get Company Info"]
        C3["🔑 Analyze Keywords"]
    end

    subgraph PHASE4["📊 PHASE 4: Qualification"]
        direction LR
        D1["🧮 Calculate Score"]
        D2["🏷️ Assign Tier"]
        D3["💡 Generate Recommendations"]
    end

    subgraph PHASE5["🚀 PHASE 5: Sales Action"]
        direction LR
        E1["📋 Review Leads"]
        E2["📧 Personalized Outreach"]
        E3["🤝 Create Opportunity"]
    end

    A1 --> B1
    A2 --> B1
    A3 --> B1
    B1 --> B2
    B2 --> C1
    C1 --> C2
    C2 --> C3
    C3 --> D1
    D1 --> D2
    D2 --> D3
    D3 --> E1
    E1 --> E2
    E2 --> E3

    style PHASE1 fill:#e8f5e9,stroke:#4caf50,stroke-width:2px
    style PHASE2 fill:#e3f2fd,stroke:#2196f3,stroke-width:2px
    style PHASE3 fill:#fff3e0,stroke:#ff9800,stroke-width:2px
    style PHASE4 fill:#fce4ec,stroke:#e91e63,stroke-width:2px
    style PHASE5 fill:#f3e5f5,stroke:#9c27b0,stroke-width:2px
```

### Detailed Journey Steps

| Phase | Step | Actor | Description | Output |
|-------|------|-------|-------------|--------|
| **1. GitHub Activity** | ⭐ Star | User | User discovers and stars Apache Druid repo | GitHub event |
| | 👁️ Watch | User | User subscribes to repo notifications | GitHub event |
| | 🐛 Issue | User | User creates issue (bug, feature, question) | GitHub event + context |
| **2. Collection** | 📥 Extract | n8n | Pull user profile from GitHub API | Raw profile data |
| | 🆕 Delta | n8n | Compare against previous run | `is_new` flag |
| **3. Enrichment** | 💼 LinkedIn | n8n | Find and extract LinkedIn profile | Title, company, history |
| | 🏢 Company | n8n | Gather company intelligence | Size, team, budget tier |
| | 🔑 Keywords | n8n | Scan for relevant keywords | Keyword score |
| **4. Qualification** | 🧮 Score | n8n | Calculate composite score (0-100) | Lead score |
| | 🏷️ Tier | n8n | Assign Hot/Warm/Cold tier | Priority level |
| | 💡 Recommend | n8n | Generate outreach strategy | Talking points, channel |
| **5. Sales** | 📋 Review | Sales | Review qualified leads in dashboard | Prioritized list |
| | 📧 Outreach | Sales | Send personalized message | Initial contact |
| | 🤝 Opportunity | Sales | Convert to sales opportunity | Pipeline entry |

### Lead Transformation Example

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        LEAD TRANSFORMATION EXAMPLE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  GITHUB USER                    ENRICHED LEAD                QUALIFIED LEAD │
│  ───────────                    ─────────────                ────────────── │
│                                                                             │
│  @john_doe          ──►         John Doe              ──►    🔥 HOT LEAD   │
│  ⭐ Starred repo               Data Engineer                 Score: 82/100 │
│  Bio: "Data stuff"             @ Acme Corp (500 emp)                        │
│                                LinkedIn: ✓                   Outreach:      │
│                                Keywords: druid, flink        → LinkedIn DM  │
│                                                              → Talk: Druid  │
│                                                                 migration   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Conversion Funnel

```mermaid
flowchart TB
    subgraph Funnel["Lead Conversion Funnel"]
        F1["👥 15,000+ GitHub Users<br/>(Stargazers + Watchers + Issue Creators)"]
        F2["📊 ~12,000 with Profiles<br/>(80% data completeness)"]
        F3["💼 ~6,000 with LinkedIn<br/>(50% enriched)"]
        F4["🔥 ~1,500 Hot Leads<br/>(Score > 70)"]
        F5["🤝 ~150 Opportunities<br/>(10% conversion)"]
        F6["💰 ~30 Deals<br/>(20% close rate)"]
    end

    F1 --> F2
    F2 --> F3
    F3 --> F4
    F4 --> F5
    F5 --> F6

    style F1 fill:#e3f2fd,stroke:#1976d2
    style F2 fill:#e8f5e9,stroke:#388e3c
    style F3 fill:#fff8e1,stroke:#ffa000
    style F4 fill:#ffebee,stroke:#d32f2f
    style F5 fill:#f3e5f5,stroke:#7b1fa2
    style F6 fill:#e8f5e9,stroke:#2e7d32,stroke-width:3px
```

---

## n8n Workflow Architecture

```mermaid
flowchart LR
    subgraph Trigger["🚀 Triggers"]
        SCHED["⏰ Scheduled<br/>(Daily/Weekly)"]
        MANUAL["👆 Manual<br/>On-Demand"]
    end

    subgraph Main["🎯 Main Orchestrator"]
        START["Start"] --> W1
        W1["GitHub Collection<br/>Sub-workflow"] --> W2
        W2["Delta Detection<br/>Sub-workflow"] --> W3
        W3["Social Enrichment<br/>Sub-workflow"] --> W4
        W4["Analysis & Scoring<br/>Sub-workflow"] --> W5
        W5["Output Generation<br/>Sub-workflow"] --> END["Complete"]
    end

    SCHED --> START
    MANUAL --> START
```

---

## Data Collection Pipeline

```mermaid
flowchart TB
    subgraph GitHub["GitHub Data Collection"]
        API["GitHub API"] --> STARS["Get Stargazers<br/>~13,000+ users"]
        API --> WATCH["Get Watchers<br/>~500+ users"]
        API --> ISSUES["Get Issue Creators<br/>~2,000+ users"]
        
        STARS --> MERGE["Merge & Deduplicate"]
        WATCH --> MERGE
        ISSUES --> MERGE
        
        MERGE --> PROFILE["Enrich Profiles<br/>Name • Bio • Company • Email"]
    end

    subgraph Delta["Delta Detection"]
        PROFILE --> COMPARE["Compare with<br/>Previous Run"]
        STORE[("Previous<br/>User IDs")] --> COMPARE
        COMPARE --> FLAG["Flag New Leads<br/>is_new = true"]
        FLAG --> UPDATE["Update Storage"]
        UPDATE --> STORE
    end

    FLAG --> OUTPUT["To Enrichment"]
```

---

## Lead Scoring Algorithm

```mermaid
pie title Lead Score Composition (100 points)
    "Keyword Relevance" : 25
    "Job Title Relevance" : 20
    "Company Potential" : 20
    "Engagement Level" : 20
    "Recency" : 15
```

### Scoring Factors

| Factor | Weight | Description |
|--------|--------|-------------|
| **Keyword Relevance** | 25% | Presence of keywords: druid, flink, starrocks, data engineering, real-time analytics |
| **Job Title** | 20% | Relevance of current role: Data Engineer, Analytics Engineer, CTO, VP Engineering |
| **Company Potential** | 20% | Company size and data team composition |
| **Engagement Level** | 20% | Issue Creator (100) > Watcher (70) > Stargazer (40) |
| **Recency** | 15% | How recently the user engaged with the repo |

### Lead Tiers

| Tier | Score Range | Action |
|------|-------------|--------|
| 🔥 **Hot** | 70-100 | Immediate outreach priority |
| 🌡️ **Warm** | 40-69 | Schedule follow-up |
| ❄️ **Cold** | 0-39 | Nurture campaign |

---

## Keyword Analysis

```mermaid
flowchart LR
    subgraph Sources["Profile Sources"]
        BIO["GitHub Bio"]
        TITLE["Job Title"]
        HEAD["LinkedIn Headline"]
        SUMMARY["LinkedIn Summary"]
        HISTORY["Work History"]
    end

    subgraph Keywords["Keyword Tiers"]
        HIGH["🔴 High Relevance<br/>druid, apache druid"]
        MED["🟡 Medium Relevance<br/>flink, starrocks, clickhouse<br/>real-time analytics"]
        STD["🟢 Standard Relevance<br/>data engineering, OLAP<br/>data warehouse, big data"]
    end

    subgraph Scoring["Location Weights"]
        W1["Job Title: 3.0x"]
        W2["Headline: 2.5x"]
        W3["Company: 2.0x"]
        W4["Bio: 1.5x"]
        W5["Summary: 1.0x"]
        W6["Work History: 0.5x"]
    end

    Sources --> Keywords
    Keywords --> Scoring
    Scoring --> FINAL["Final Keyword Score<br/>(0-100)"]
```

---

## Company Intelligence

```mermaid
flowchart TB
    subgraph Input["Company Identification"]
        GH_CO["GitHub Profile<br/>Company Field"]
        LI_CO["LinkedIn<br/>Current Company"]
    end

    subgraph Lookup["Data Enrichment"]
        CLEARBIT["Clearbit API"]
        CRUNCH["Crunchbase"]
        LI_PAGE["LinkedIn Company Page"]
    end

    subgraph Output["Intelligence Output"]
        SIZE["Company Size<br/>Employee Count"]
        TEAM["Data Team Size<br/>Estimated"]
        BUDGET["Budget Tier<br/>Low/Med/High/Enterprise"]
        IND["Industry"]
    end

    Input --> LOOKUP["Normalize &<br/>Lookup"]
    LOOKUP --> Lookup
    Lookup --> Output
```

### Company Size Categories

| Category | Employee Count | Budget Tier |
|----------|---------------|-------------|
| Startup | 1-50 | Low |
| Small | 51-200 | Medium |
| Medium | 201-1,000 | High |
| Large | 1,001-5,000 | High |
| Enterprise | 5,000+ | Enterprise |

---

## Output: Lead Record Structure

```mermaid
classDiagram
    class ScoredLead {
        +string username
        +string name
        +string email
        +string company
        +string location
        +string source
        +boolean is_new
        +date first_seen_date
        +string linkedin_url
        +string twitter_url
        +string current_title
        +string current_company
        +KeywordAnalysis keyword_analysis
        +CompanyIntel company_intel
        +number composite_score
        +ScoreBreakdown score_breakdown
        +string tier
        +OutreachRecommendation outreach
    }

    class KeywordAnalysis {
        +number keyword_score
        +KeywordMatch[] matched_keywords
        +number total_matches
    }

    class CompanyIntel {
        +string company_size
        +number employee_count
        +number data_team_size
        +string estimated_budget
    }

    class OutreachRecommendation {
        +string recommended_channel
        +string urgency
        +string[] talking_points
        +string[] personalization_hooks
    }

    ScoredLead --> KeywordAnalysis
    ScoredLead --> CompanyIntel
    ScoredLead --> OutreachRecommendation
```

---

## Error Handling & Recovery

```mermaid
flowchart TD
    START["API Request"] --> CHECK{"Response?"}
    
    CHECK -->|"Success"| CONTINUE["Continue Processing"]
    CHECK -->|"Rate Limit (429)"| WAIT["Wait for Reset"]
    CHECK -->|"Server Error (5xx)"| RETRY["Retry with Backoff"]
    CHECK -->|"Not Found (404)"| SKIP["Skip & Log"]
    CHECK -->|"Auth Error (401)"| HALT["Halt & Alert"]
    
    WAIT --> START
    RETRY -->|"Max 3 retries"| SKIP
    RETRY -->|"Success"| CONTINUE
    
    SKIP --> SAVE["Save Checkpoint"]
    SAVE --> NEXT["Next Record"]
    
    HALT --> NOTIFY["Send Alert"]
    NOTIFY --> CHECKPOINT["Save Progress"]
```

---

## Implementation Phases

```mermaid
gantt
    title Implementation Timeline
    dateFormat  YYYY-MM-DD
    section Phase 1: Foundation
    Project Setup & Config       :p1, 2026-01-29, 2d
    GitHub Data Collection       :p2, after p1, 3d
    Delta Detection              :p3, after p2, 2d
    
    section Phase 2: Enrichment
    Social Profile Discovery     :p4, after p3, 3d
    LinkedIn Extraction          :p5, after p4, 2d
    
    section Phase 3: Analysis
    Keyword Analysis             :p6, after p5, 2d
    Company Intelligence         :p7, after p6, 2d
    Lead Scoring                 :p8, after p7, 2d
    
    section Phase 4: Output
    Output Generation            :p9, after p8, 2d
    Error Handling               :p10, after p9, 2d
    Main Orchestrator            :p11, after p10, 2d
    
    section Phase 5: Documentation
    Documentation                :p12, after p11, 3d
    Testing & Validation         :p13, after p12, 3d
```

---

## Expected Outcomes

| Metric | Expected Value |
|--------|---------------|
| **Total Leads Collected** | ~15,000+ unique users |
| **New Leads per Run** | ~50-200 (depending on frequency) |
| **Hot Leads** | ~5-10% of total |
| **Warm Leads** | ~20-30% of total |
| **Data Completeness** | ~60-80% average |
| **Processing Time** | ~2-4 hours per full run |

---

## Next Steps

1. **Review this overview** - Ensure the approach aligns with Deep.BI's sales strategy
2. **Set up n8n instance** - Self-hosted or cloud
3. **Configure API credentials** - GitHub token, enrichment APIs
4. **Start implementation** - Follow tasks in `.kiro/specs/github-lead-generation-n8n/tasks.md`
5. **Test with smaller repo** - Validate before running against Apache Druid

---

*Generated for Deep.BI Lead Generation Initiative*
