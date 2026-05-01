---
title: pg-explain-viz — visualise Postgres EXPLAIN output in browser
date: 2024-02-22
stack: typescript
description: Web tool · D3.js · paste your EXPLAIN ANALYZE output and see it as a tree
repo: https://github.com/jai7/pg-explain-viz
---

A browser tool that takes `EXPLAIN (ANALYZE, FORMAT JSON)` output and renders it as an interactive node tree, with cost and timing shown inline on each node.

## The problem

Reading raw `EXPLAIN ANALYZE` output is painful. The text format is fine for simple queries but becomes unreadable for plans with 20+ nodes. I wanted something like the pgAdmin visual explain but that works in any browser without a server.

## Stack

Pure TypeScript, D3.js for the tree layout, no backend. You paste JSON in the left panel, the tree renders on the right. Nodes are colour-coded by their share of total cost — red means expensive.

## Limitations

It doesn't handle parallel plans particularly well yet. That's the next thing to fix.
