# Section 3 – Thought Process

## Overview

This section contains reasoning-based tasks focused on incident response, debugging approach, and production decision-making.

According to the assignment, Section 3 is intended to simulate production issues and describe a structured approach to solving them.

## Available Tasks and status ✅ Done 🟡 In Progress ⚪ Not Selected Yet

-✅ `task-a/` – Production went down

-⚪ `task-b/` – CI/CD pipeline is stuck

-⚪ `task-c/` – Terraform shows large infrastructure diff unexpectedly

## Selected Task

For this section, I selected **Task A – Production went down**.

### Why I selected this task
I selected Task A because it is the most direct way to demonstrate a structured DevOps incident response process:
- confirming the incident,
- assessing impact,
- checking recent changes,
- investigating layer by layer,
- mitigating safely,
- verifying recovery,
- documenting follow-up actions.

It is also the clearest task for presenting step-by-step reasoning in a concise and production-oriented format.

## Task Summaries

### Task A – Production went down
Focus: incident triage and service restoration.

Expected approach:
- confirm the outage,
- determine impact and severity,
- review recent deployments or configuration changes,
- investigate logs, metrics, dependencies, and infrastructure,
- restore service with the lowest-risk action,
- verify recovery.

### Task B – CI/CD pipeline is stuck
Focus: debugging a hanging Jenkins or GitLab CI pipeline.

Expected approach:
- inspect pipeline stage progress,
- review runner/agent logs,
- identify blocked jobs or external dependencies,
- determine whether the issue is infrastructure, executor, or configuration related,
- unblock the pipeline safely.

### Task C – Terraform shows large infrastructure diff unexpectedly
Focus: safe Terraform decision-making before apply.

Expected approach:
- stop before approval,
- review recent code/module/provider/backend changes,
- inspect state and possible drift,
- compare expected vs unexpected plan output,
- confirm impact before applying any infrastructure change.

## Repository Notes

Each task folder in this section contains either:
- the selected task solution, or
- a placeholder README for repository completeness.

## Current Status

- `task-a/` – selected task
- `task-b/` – placeholder
- `task-c/` – placeholder

## Submission Note

This section is organized to match the required repository structure:
- `section-1/`
- `section-2/`
- `section-3/`

The selected solution for Section 3 is documented inside `task-a/README.md`.
