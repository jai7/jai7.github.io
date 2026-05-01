---
title: Internal developer platform — Acme Corp
date: 2024-01-01
tags: [infra]
status: ongoing
description: Platform that reduced deploy time 60% across an engineering org of 80 people.
tech: Go · Kubernetes · Terraform · GitHub Actions
---

Led a team of 8 to design and ship an internal developer platform that replaced a patchwork of shell scripts and manual processes.

## The problem

Deploy times averaged 45 minutes. Engineers were blocked waiting for infra changes. Staging environments were shared and flaky. New service onboarding took two weeks.

## What we built

- **Self-service environment provisioning** — engineers create isolated environments in under 3 minutes via a CLI
- **Unified deploy pipeline** — single command deploys from local to production, with automatic rollback on error rate spike
- **Service catalog** — auto-generated from code annotations; every service documents its dependencies, owners, and runbooks

## Results

- Deploy time: 45 min → 18 min (60% reduction)
- New service onboarding: 2 weeks → 2 days
- Staging environment conflicts: eliminated (each PR gets its own environment)
