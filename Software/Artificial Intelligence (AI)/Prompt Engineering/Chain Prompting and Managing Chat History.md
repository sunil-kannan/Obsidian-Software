---
date: "2026-05-15"
tags: 
link:
---
# Chain Prompting and Managing Chat History

## Idea
Long AI conversations increase token/context usage, leading to:
- higher PRU/token cost
- slower responses
- reduced reasoning quality
- outdated context pollution

## Best Practice
Instead of carrying full chat history:
- summarize previous work
- provide only relevant context
- start fresh chats for new features/debugging

## Good Prompt Style
Current system:
- Spring Boot
- JWT auth
- Redis
- PostgreSQL

Existing:
- login flow implemented
- refresh tokens implemented

Need:
- add rate limiting for brute-force prevention

## Why This Helps
- lower context usage
- faster responses
- better reasoning focus
- avoids hallucinations from old context
- keeps AI focused on current problem

## Principle
High signal, low noise.

Short focused context > huge conversation history.