---
title: What I learned running Kafka at 500k events/sec
date: 2025-01-15
tags: [kafka, infra]
description: Lessons from 18 months running a high-throughput Kafka cluster in production.
readingTime: 12 min read
---

Eighteen months ago we migrated our event pipeline to Kafka. We're now processing around 500k events per second at peak. Here's what surprised us.

## Partition count is a one-way door

You can increase partitions but you can't decrease them. We started with 12 and had to rebalance to 48 within three months as throughput grew. Plan for 3-5x your expected peak.

## Consumer lag is your most important metric

Not throughput. Not latency. Consumer lag. If it's growing, something is wrong — and it's almost never Kafka itself.

## The retention math is counterintuitive

We keep 7 days of retention across all topics. At 500k events/sec, that's roughly 300TB. The cost is high but the ability to replay any window is invaluable for debugging production incidents.

## What we got wrong

We tried to use Kafka as a database early on — reading from it as a source of truth. Don't. It's a log, not a store. Use it to feed a real read store (we use ClickHouse) and query that instead.
