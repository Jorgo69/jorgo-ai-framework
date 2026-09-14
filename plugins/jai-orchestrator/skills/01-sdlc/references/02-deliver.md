# 02 - Deliver

## Behavior

Present the plan to the user and wait for explicit approval before handing it to an executor. Once approved, give the executor the plan. The executor implements it and calls the validation skills, which own their checks and repair loops. Include architecture conformance whenever the project documents architecture. Run a required end-to-end journey after every other validation.

Call the commit skill in `interactive` mode, never `auto`: it stages the change, drafts the conventional message, and pauses for the user's explicit approval before committing or pushing. Only send the approved, committed candidate to Check.

```mermaid
---
title: Deliver the candidate
---
flowchart TD
  subgraph PlanStage["Plan the delivery"]
    direction TB
    Contract["$contract"]
    Plan["/jai-dev:01-plan"]
    PlanArtifact["$plan"]
    PlanApproval{{"User approves plan?"}}
  end

  subgraph ExecuteStage["Execute and validate the plan"]
    direction TB
    Executor(["@jai-dev:executor"])
    Implement["/jai-dev:02-implement"]
    Assert["/jai-dev:03-assert"]
    Test["/jai-dev:06-test"]
    Commit["/jai-vcs:01-commit interactive"]
    CommitApproval{{"User approves diff + message?"}}
  end

  subgraph HandoffStage["Hand off the candidate"]
    direction TB
    CommittedCandidate["$committed_candidate"]
    Check["03 Check"]
  end

  Contract --> Plan
  Plan --> PlanArtifact
  PlanArtifact --> PlanApproval
  PlanApproval -- "No: revise with Frame" --> Contract
  PlanApproval -- "Yes" --> Executor
  Executor --> Implement
  Implement --> Assert
  Assert -- "When no end-to-end journey is required, stage the commit." --> Commit
  Assert -- "When an end-to-end journey is required, run it last." --> Test
  Test -- "After the journey succeeds, stage the commit." --> Commit
  Test -- "Return a failed journey for repair." --> Executor
  Commit --> CommitApproval
  CommitApproval -- "No: keep working, do not push" --> Executor
  CommitApproval -- "Yes: commit and push" --> CommittedCandidate
  CommittedCandidate --> Check

  classDef skill fill:#DBEAFE,stroke:#2563EB,color:#1E3A8A,stroke-width:2px
  classDef agent fill:#F3E8FF,stroke:#9333EA,color:#581C87,stroke-width:2px
  classDef artifact fill:#DCFCE7,stroke:#16A34A,color:#14532D,stroke-width:2px
  classDef zone fill:#F1F5F9,stroke:#64748B,color:#0F172A,stroke-width:2px
  classDef gate fill:#FEF3C7,stroke:#D97706,color:#78350F,stroke-width:2px

  class Plan,Implement,Assert,Test,Commit skill
  class Executor agent
  class Contract,PlanArtifact,CommittedCandidate artifact
  class Check zone
  class PlanApproval,CommitApproval gate
```
