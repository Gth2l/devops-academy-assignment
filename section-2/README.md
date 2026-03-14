# Section 2 – Troubleshooting

## Overview

This section contains troubleshooting tasks focused on diagnosing and fixing realistic DevOps issues in application runtime, container builds, Terraform workflows, and Kubernetes workloads.

The objective of this section is to demonstrate:
- structured debugging,
- root cause analysis,
- safe remediation,
- verification of the fix,
- prevention recommendations.

## Available Tasks and status   ✅ Done 🟡 In Progress ⚪ Not Selected Yet

-✅ `task-a/` – 502 Bad Gateway (Nginx + Node.js) 

-✅ `task-b/` – Terraform Error: Error locking state 

-⚪ `task-c/` – Docker Build Fails (`no space left on device`)

-⚪ `task-d/` – Pod in CrashLoopBackOff (Node.js App)

-✅ `task-e/` – Secret Not Mounted as ENV (Kubernetes)




## Recommended Troubleshooting Structure

Each selected task in this section should be documented using the following structure:

### 1. Problem Summary
What is broken and how the issue appears.

### 2. Investigation
What was checked first and how the issue was narrowed down.

### 3. Root Cause
The exact technical reason for the failure.

### 4. Fix
The change required to resolve the problem.

### 5. Verification
Commands, logs, or checks confirming the issue is fixed.

### 6. Prevention
Measures that would reduce the chance of the same issue happening again.

## Task Summaries

### Task A – 502 Bad Gateway
Focus:
- diagnose reverse proxy misconfiguration,
- identify service/port mismatch,
- correct upstream connectivity.

### Task B – Terraform Error: Error locking state
Focus:
- explain state locking behavior,
- identify why locking fails,
- propose short-term and long-term fixes,
- define safer team Terraform workflows.

### Task C – Docker Build Fails (`no space left on device`)
Focus:
- investigate CI disk exhaustion,
- identify build/cache/storage pressure,
- propose temporary cleanup and long-term capacity controls,
- recommend monitoring.

### Task D – Pod in CrashLoopBackOff
Focus:
- identify why the application keeps crashing,
- inspect pod logs and restart behavior,
- improve observability through logs and probes,
- recommend more stable crash handling.

### Task E – Secret Not Mounted as ENV
Focus:
- determine why the secret value is missing at runtime,
- identify namespace or resource mismatch,
- verify secret usage safely without exposing sensitive values.

## Current Status

This section is prepared for the selected troubleshooting task and supporting documentation.

Task folders are organized for clean submission and repository structure consistency.

## Submission Note

This repository follows the required structure:
- `section-1/`
- `section-2/`
- `section-3/`

The final selected troubleshooting solution should be documented inside the relevant task folder in this section.
