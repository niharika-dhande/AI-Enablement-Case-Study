# Does this need AI?

**Pipeline step:** 4 and 5 · Use before any use case enters a build cycle.

```mermaid
flowchart TD
    R["Request from a team"] --> P{"Is the workflow<br/>predictable and<br/>rule-based?"}
    P -- "Yes" --> AUTO["Traditional automation:<br/>API, scheduler, script"]
    P -- "No" --> U{"Does it involve unstructured<br/>text, natural-language questions,<br/>summaries or retrieval?"}
    U -- "Yes" --> K{"Does it need the<br/>company's own<br/>knowledge?"}
    K -- "Yes" --> RAG["RAG solution"]
    K -- "No" --> LLM["LLM workflow,<br/>skill or agent"]
    U -- "No" --> AUTO
    RAG --> S{"Would a simple<br/>integration solve it<br/>reliably anyway?"}
    LLM --> S
    S -- "Yes" --> AUTO
    S -- "No" --> BUILD["Build it: baseline,<br/>2-week cycle"]
```

## Checklist

- [ ] The task is not fully predictable with fixed rules
- [ ] It involves unstructured text, language understanding, summarisation or retrieval
- [ ] A simple workflow or API integration would not solve it reliably
- [ ] There is a baseline to beat (time, effort, accuracy or cost)
- [ ] The data it touches can be used on the chosen platform
- [ ] Someone on the team will own and maintain it after rollout

If any of the first three boxes is unticked, recommend the simpler option. AI adds complexity, cost and unpredictability, so it has to earn its place.
