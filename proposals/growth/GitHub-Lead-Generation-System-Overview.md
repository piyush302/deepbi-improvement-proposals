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

```mermaid
journey
    title Lead Generation User Journey
    section GitHub Activity
      User stars Apache Druid repo: 5: Potential Lead
      User watches Apache Druid repo: 5: Potential Lead
      User creates issue on repo: 5: Potential Lead
    section Automated Collection
      Workflow extracts user profile: 3: n8n System
      Delta detection flags new user: 3: n8n System
    section Profile Enrichment
      LinkedIn profile discovered: 3: n8n System
      Company intelligence gathered: 3: n8n System
      Keywords analyzed: 3: n8n System
    section Lead Qualification
      Composite score calculated: 3: n8n System
      Lead tier assigned (Hot/Warm/Cold): 3: n8n System
      Outreach recommendations generated: 3: n8n System
    section Sales Action
      Sales reviews qualified leads: 5: Sales Team
      Personalized outreach initiated: 5: Sales Team
      Deal opportunity created: 5: Sales Team
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
