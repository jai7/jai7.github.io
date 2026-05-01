---
title: Observability is not monitoring — and the difference matters
date: 2024-09-08
tags: [observability, infra]
description: Why the distinction between monitoring and observability changes how you build systems.
readingTime: 7 min read
---

Monitoring tells you when something is wrong. Observability tells you why.

Monitoring is a set of known questions asked repeatedly: is the error rate above 1%? Is p99 latency above 500ms? These are useful but they only catch failure modes you anticipated when you wrote the alert.

Observability means your system emits enough signal that you can ask questions you didn't think of at build time. High cardinality traces, structured logs with rich context, metrics that can be sliced by arbitrary dimensions.

## The practical difference

With monitoring: your on-call gets paged, looks at dashboards, and tries to correlate pre-built charts.

With observability: your on-call gets paged, queries the trace data directly, and finds the exact request that triggered the issue — including the user ID, the specific code path, and the database query that was slow.

## What good looks like

Every request should carry a trace ID from edge to storage. Every log line should include that trace ID. Every slow query should be automatically annotated with the context that called it.

This is not free to build. But it's far cheaper than the alternative: three engineers spending six hours debugging a production incident with `tail -f` and prayer.
