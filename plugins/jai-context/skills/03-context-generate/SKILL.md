---
name: 03-context-generate
description: Route a request to generate a context artifact (skill, rule, agent, command, or hook) to its generator when the kind is unnamed. A named kind triggers its generator directly. Not for listing existing artifacts.
argument-hint: skill | rule | agent | command | hook
---

# Context Generate

Routes a generation request to the dedicated generator for the artifact kind. Holds no generation logic of its own.

## Routing

| Artifact | Generator                        |
| -------- | -------------------------------- |
| skill    | `jai-context:04-skill-generate` |
| rule     | `jai-context:05-rule-generate`  |
| agent    | `jai-context:06-agent-generate` |
| command  | `jai-context:07-command-generate` |
| hook     | `jai-context:08-hook-generate`  |

Identify the artifact kind from the request, then hand off to the matching generator. If the kind is unclear, ask which one. To survey or list existing artifacts, use the explore skill instead.
