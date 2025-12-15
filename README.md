# Risk Guard (VS Code Extension)

Engineers, reviewers, and infra teams who want to spot risky diffs **before they land**.

Risk Guard scans your **git diff** inside VS Code and surfaces risky changes directly in the **Problems panel**, so you can fix issues early—before commit or PR.

---

## What is Risk Guard?

Risk Guard is a VS Code extension that inspects Git diffs (staged or unstaged) and flags **potentially dangerous edits** as editor diagnostics.

It is designed for application and infrastructure code where small changes can cause production incidents.

---

## Why Risk Guard exists（解決したい問題）

- **Prevent incidents early**  
  Catch risky infrastructure or configuration changes before they reach production.

- **Reduce reviewer load**  
  Filter out obvious hazards locally so reviewers can focus on higher-level logic.

- **Fast feedback for authors**  
  Get immediate signals on save or before committing, without waiting for CI or review.

---

## How it works  
**git diff → rule-based analysis → Problems**

1. Reads the current Git diff in your workspace  
   - unstaged (`git diff`)  
   - staged (`git diff --cached`, optional)

2. Applies **deterministic, rule-based checks**  
   - no AI decisions  
   - no external services  
   - fully offline

3. Reports findings as diagnostics in the **Problems panel**, with file/line navigation.

---

## Features

- **Diff-native detection**  
  Analysis is based on *what changed*, not the full file.

- **Infrastructure-focused rules**  
  Examples:
  - Public ingress (SSH / RDP / open ports)
  - Privileged Kubernetes pods
  - Missing resource limits in K8s
  - IAM wildcard permissions
  - S3 / RDS hardening regressions
  - Disabled logging or audit settings
  - Plaintext secrets in diffs

- **Multiple trigger modes**
  - On save
  - On demand (Command Palette)
  - Background timer

- **Lightweight & offline**
  - No telemetry
  - No network calls
  - Safe for restricted environments

- **Future-ready**
  - Optional AI-assisted *explanations* are planned
  - Detection logic will remain deterministic by default

---

## Usage

### For users
1. Install **Risk Guard** from the VS Code Marketplace.
2. Open a Git repository and modify files.
3. Save a file or run `Risk Guard: Scan Git Diff`.
4. Open the **Problems panel** to review issues and jump to the exact lines.

### For development
```bash
npm install
npm run compile
Press F5 to launch the Extension Development Host.

Settings
You can configure Risk Guard in
VS Code → Settings → Extensions → Risk Guard

riskGuard.useStagedDiff
Scan staged changes (git diff --cached) instead of unstaged
Default: false

riskGuard.scanIntervalSeconds
Background scan interval (minimum 5 seconds)
Default: 30

Design philosophy
Fail early, locally, and deterministically

Prefer explainable rules over opaque heuristics

Optimize for real-world infra mistakes, not academic linting



