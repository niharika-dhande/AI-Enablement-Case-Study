# 2. The execution pipeline

Ten steps, run in order for the first segment and then repeated as a loop for every new use case. Each step has an owner, an input, an output and an exit check. A step is not finished until its exit check passes.

```mermaid
flowchart TD
    subgraph P1["Phase 1: Understand"]
        S1["1. Discover"] --> S2["2. Baseline"]
    end
    subgraph P2["Phase 2: Design"]
        S3["3. Segment"] --> S4["4. Segment R&D"]
    end
    subgraph P3["Phase 3: Build"]
        S5["5. Build PoC / MVP"] --> S6["6. Dogfood"]
    end
    subgraph P4["Phase 4: Roll out"]
        S7["7. Segment pilot"] --> S8["8. Enterprise distribution"] --> S9["9. Train and support"]
    end
    subgraph P5["Phase 5: Prove"]
        S10["10. Measure"]
    end
    S2 --> S3
    S4 --> S5
    S6 --> S7
    S9 --> S10
    S10 -. "new use case" .-> S4
    S6 -. "fails internal use" .-> S5
```

## Step by step

| # | Step | Owner | Input | Output | Exit check |
|---|---|---|---|---|---|
| 1 | **Discover** | Me | Time with each team, as part of the team | List of bottlenecks per role | Every role has its top time-wasters written down |
| 2 | **Baseline** | Me with the team | Bottleneck list | Hours, accuracy and cost per task today | Each target task has a "before" number |
| 3 | **Segment** | Me | Roles, work types, security needs | Four tracks: Developers, QA, UI/UX, BA/PM/docs | Every person belongs to exactly one track |
| 4 | **Segment R&D** | Me with the enablement team | One track's bottlenecks | Use cases, model tier, tool shape for that track | Each use case passes the [does this need AI?](../playbook/04-does-this-need-ai.md) test |
| 5 | **Build PoC / MVP** | Enablement team (developers and testers) | Chosen use case | Working RAG app, agent, skill, Claude project or connector | Built and tested inside a 2-week cycle |
| 6 | **Dogfood** | Enablement team | PoC / MVP | The enablement team's own daily use | Works in real work, issues fixed |
| 7 | **Segment pilot** | Me with the track | Dogfooded tool | Tool in use by one track | Track uses it on live work |
| 8 | **Enterprise distribution** | Me | Piloted tool | Tool published through the right channel | Anyone in the track can reach it without help |
| 9 | **Train and support** | Me | Published tool | Hands-on sessions, support during adoption | People use it without asking how |
| 10 | **Measure** | Me with the team | Usage and task data | "After" numbers against the baseline | Clear keep, improve or retire decision |

## How the phases ran over time

The first track went through every step. Later tracks reused what already existed, so they moved faster. From the first team to company-wide use took about 6–12 months.

```mermaid
timeline
    title Gate6 rollout (about 6–12 months in total)
    Understand : Sit with each team : Write down bottlenecks : Baseline the target tasks
    Design : Split into 4 tracks : R&D per track : Match model tier to track
    Build : 2-week PoC cycles : Enablement team dogfoods every tool
    Roll out : Pilot with one track : Publish through 4 channels : Hands-on training
    Scale : Teams build their own agents : Hundreds of agents across the SDLC
```

## Why this order works

- **Discover before segmenting.** The tracks came from where time was actually lost, not from the org chart.
- **Baseline before building.** Without a "before" number there is no way to prove anything after.
- **Dogfood before pilot.** The enablement team always used a tool on its own work first, so other teams never received a tool that had only been demoed.
- **Pilot one track before distributing.** Problems showed up with one group, not the whole company.
- **The loop.** Once a track was enabled, new use cases from that track went straight back into segment R&D. By the end the teams were building their own agents.

[← Context](01-context-and-problem.md) · [Next: segments and model tiers →](03-segments-and-model-tiers.md)
