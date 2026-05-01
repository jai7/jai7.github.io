---
title: Why I stopped using ORMs for analytical queries
date: 2025-04-18
tags: [data, postgres]
description: After three years of fighting my ORM on anything beyond simple CRUD, I finally gave up.
readingTime: 8 min read
---

After three years of fighting my ORM on anything beyond simple CRUD, I finally gave up and went raw SQL for all analytical queries. Here's what I learned.

## The problem

ORMs are great at what they're designed for: mapping rows to objects, handling simple CRUD, and abstracting away database differences. But the moment you need a window function, a lateral join, or a complex aggregation, you're fighting the tool.

```sql
SELECT
  user_id,
  event_type,
  COUNT(*) OVER (PARTITION BY user_id ORDER BY created_at) as running_total
FROM events
WHERE created_at > NOW() - INTERVAL '30 days'
```

Try expressing that cleanly in most ORMs. You can't — not without dropping to raw SQL anyway, at which point you've lost the benefit.

## What I switched to

Raw SQL with a thin query builder for the dynamic parts. The key insight: **the abstraction you actually need is parameterized queries, not object mapping**.

## What I kept the ORM for

- Simple CRUD on known entities
- Schema migrations (the ORM's migration tools are still excellent)
- Seeding test data

The rest is plain SQL, wrapped in typed functions that validate the output shape.
