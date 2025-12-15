# Risk Guard (VS Code Extension)

**Spot risky git diffs before they land.**  
Risk Guard scans your **staged/unstaged diffs** inside VS Code and surfaces hazards in the **Problems** panel, so you can fix issues **before commit / PR**.

## What it does
- Diff-first detection (analyzes what changed)
- Deterministic, rule-based checks (offline by default)
- Reports findings as VS Code diagnostics with file/line navigation

## Why
Small infra/config diffs can cause production incidents. CI and PR reviews are often too late and too noisy. Risk Guard gives fast local feedback at the moment you change code.

## How it works
`git diff` → rule-based analysis → VS Code **Problems**

- Unstaged: `git diff`
- Staged (optional): `git diff --cached`
- No network calls, no telemetry

## Example rules (early MVP)
- Public ingress / open ports (SSH/RDP, 0.0.0.0/0)
- Kubernetes privileged pods / missing resource limits
- IAM wildcard permissions
- Logging/audit disabled
- Plaintext secrets in diffs

## Usage
### For development
```bash
npm install
npm run compile
