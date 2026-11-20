# 4. Build, test and release

## The enablement team

I set up a small enablement team of developers and testers. Testers were part of the team from day one, not added at the end. Together we built every PoC and MVP, tested it, and used it ourselves before any other team saw it.

I personally designed and delivered 30+ of these PoCs, running 2-week delivery cycles: sprint planning, backlog refinement, demos and retrospectives.

## From idea to a tool other engineers can maintain

```mermaid
flowchart LR
    U["Use case from<br/>segment R&D"] --> B["Build PoC<br/>in a 2-week cycle"]
    B --> T["Test inside the<br/>enablement team"]
    T --> DF["Use it on our<br/>own daily work"]
    DF --> OK{"Robust and<br/>maintainable?"}
    OK -- "No" --> B
    OK -- "Yes" --> P["Pass to one<br/>segment as a pilot"]
    P --> I["Integrate into the<br/>regular pipelines"]
```

The rule was simple: a tool left the enablement team only when another engineer could safely take it over and maintain it, and when it could plug into the team's regular pipeline.

## What we built

| Kind of tool | Example |
|---|---|
| **Agent** | A Jira agent that pulls all stories and boards needed for a release |
| **RAG app** | Question answering over project documents and knowledge |
| **Sub-agent skills** | Reusable skills for SDLC and documentation tasks |
| **Claude projects** | Team projects with shared instructions and knowledge |
| **Connectors and plugins** | Our tools exposed inside Claude |
| **Prompt libraries** | Reusable prompts and agent patterns |

## Where AI sits in the SDLC

```mermaid
flowchart LR
    R["Requirements<br/>Jira agent,<br/>story writing"] --> DS["Design<br/>AI-assisted<br/>prototyping"]
    DS --> DV["Development<br/>Claude Code,<br/>BMAD specs, skills"]
    DV --> TS["Testing<br/>test case<br/>generation"]
    TS --> DC["Documentation<br/>business docs,<br/>release notes"]
    DC --> RL["Release<br/>Jira agent pulls<br/>release scope"]
```

## Data quality for RAG tools

Every RAG tool went through the same cleaning pipeline before anything reached the vector store. Most bad answers in RAG come from bad data, not from the model.

```mermaid
flowchart TD
    C["Collect all source data"] --> R["Remove repeated content<br/>headers, footers, repeated<br/>CTA sections from scraped pages"]
    R --> Q["Separate inconsistent and<br/>poor-quality data"]
    Q --> CO["Check consistency"]
    CO --> F["Check freshness"]
    F --> V{"Chunking, embedding and<br/>ingestion work well<br/>on this data?"}
    V -- "No" --> R
    V -- "Yes" --> VS["Store in the vector store"]
    VS --> RET["Start retrieval"]
```

## When AI output turns inconsistent

Once tools were in daily use, the most common complaint was "it gave me something different this time". I debugged it in this order:

```mermaid
flowchart TD
    I["Inconsistent output<br/>reported"] --> L{"Very long session?"}
    L -- "Yes" --> L1["Start a fresh session.<br/>Long sessions drift into<br/>their own patterns"]
    L -- "No" --> U{"Skill or agent<br/>recently updated?"}
    U -- "Yes" --> U1["Check what changed<br/>in the skill or agent"]
    U -- "No" --> M{"Memory carrying<br/>old context?"}
    M -- "Yes" --> M1["Clean up memory"]
    M -- "No" --> D["RAG tool: check chunks,<br/>vectors and ingestion"]
```

[← Segments and model tiers](03-segments-and-model-tiers.md) · [Next: enterprise distribution →](05-enterprise-distribution.md)
