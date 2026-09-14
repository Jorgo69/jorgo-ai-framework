---
name: 01-hello
description: Smoke-test that confirms the jai-ui plugin loads. Use when the user wants to verify the alpha jai-ui plugin is installed and reachable. Not for real UI or UX design work.
---

# Skill: hello

Confirm the jai-ui plugin loads and is reachable.

## Actions

| #   | Action  | Role                                        |
| --- | ------- | ------------------------------------------- |
| 01  | `greet` | Greet the user and confirm the skill works  |

Single action skill: run `greet` and return its message.
Before running an action, read its file in `actions/`, not only the table or assets.

## Prerequisites

- The plugin loaded locally (`claude --plugin-dir plugins/jai-ui`, or installed from the marketplace).
