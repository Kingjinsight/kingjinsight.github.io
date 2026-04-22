---
date: "2026-03-11"
draft: false
title: 'Context Engineering'
author: 'King Jin'
tags: ["AI","Engineering"]
showtoc: true
---

We have several parts in context:
- System prompt
- User Prompt
- Dialogue history
- Memory
- Relavent information from other sources
- Tool use
- Reasoning

## What is context engineering
**Prompt Engineering** is about how to write instructions. **Context Engineering** is broader - it covers strategies for curating and maintaining the optimal set of tokens during inference, including everything that lands in context window beyond just the system prompt: tools, MCP servers, Skills, external data, message history and so on.

## System prompt
Claude's system prompt: [link](https://platform.claude.com/docs/en/release-notes/system-prompts)

## Context Retrieval
- Just in time context strategies
- Rather than pre-loading all relevant data up front, agents maintain lightweight identifiers(file paths, stored queries, web links) and dynamically load data into context at runtime using tools.

## Long-Horizon Tasks: Three techniques
- Compaction
	- It takes a conversation nearing the context window limit, summarizes it, and reinitializes a new context window with the summary.
	- The art lies in selecting what to keep vs. discard, overly aggressive compaction can lose subtle but critical context. Anthropic recommends starting by maximizing recall.
- Structured Note-Taking
	- It involves the agent regularly writing notes persisted to memory outside the context window, which get pulled back in later.

- Sub-Agent Architectures
	- Rather than one agent maintaining state across an entire project, specialized sub-agents handle focus tasks with clean context windows. The main agent coordinates with a high-level plan while sub-agents perform deep technical work. Each sub-agent may use tens of thousands of tokens in its exploration but returns only a condensed summary of 1,000–2,000 tokens to the lead agent — achieving a clear separation of concerns.

## My understanding
Write good and precise prompt at beginning. Just-in-time strategies is clever, it just work like human brain, when we need a reference/tool, we take it, otherwise we place it in somewhere, rather than memorized all these resources.
