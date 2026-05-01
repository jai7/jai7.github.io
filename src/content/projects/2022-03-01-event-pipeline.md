---
title: Real-time event pipeline at Startup XYZ
date: 2022-03-01
tags: [data]
status: shipped
description: 500k events/sec pipeline built on Kafka, Flink and ClickHouse.
tech: Kafka · Apache Flink · ClickHouse · Go
---

Designed and built the core event ingestion and processing pipeline that powered all analytics and real-time features across the product.

## Scale

- 500,000 events per second at peak
- 300TB of 7-day retention in Kafka
- Sub-second latency from event emission to dashboard update

## Architecture

Events are emitted from services via a thin Go client that batches and compresses before sending to Kafka. Flink jobs consume from Kafka, apply transformations and enrichments, and write to ClickHouse for analytics and to Postgres for operational queries.

## The hardest part

Schema evolution. When you have 50 services emitting to 30 topics, any schema change is a coordination problem. We ended up building a schema registry with backwards-compatibility enforcement — producers can't push breaking changes without a migration path.

## What I'd do differently

Start with a schema registry on day one, not month eighteen.
