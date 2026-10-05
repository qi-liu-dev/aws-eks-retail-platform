# AGENTS.md

## Project
Platform work for AWS's open-source Retail Store Sample App (../retail-store-sample-app).
I did not write the app. This repo holds my infrastructure, deployment, CI/CD,
observability and docs. Current phase and status: docs/progress.md.

## Rules
- One phase at a time. Explain what we'll build and why, state done criteria, then implement and verify.
- Do not modify ../retail-store-sample-app unless I ask, and only on a feature branch.
- Never run terraform apply, eksctl, or AWS CLI commands that create resources without my explicit approval.
  Before any billable step, say so and estimate the hourly cost.
- Say where upstream file paths, Helm values and Terraform variables come from.
  If you haven't read the file, say so instead of guessing.
- Record meaningful decisions in docs/decisions/ (context, options, choice, consequences).
- Keep a README section listing what came from AWS and what I changed.
- Don't add tools just for keywords. Never write resume bullets for unfinished work.