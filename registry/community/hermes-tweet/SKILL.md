---
name: hermes-tweet
version: '0.1.6'
description: Use Hermes Tweet to read sourced X/Twitter profiles, timelines, searches, and post URLs, with posting actions gated by explicit env opt-in.
author: Xquik-dev
namespace: community
category: social-automation
tags: [hermes-agent, twitter, x, social-listening, social-research]
requires_secrets: [XQUIK_API_KEY]
requires_tools: []
metadata:
  agentos:
    homepage: https://github.com/Xquik-dev/hermes-tweet
---

# Hermes Tweet

You can use this skill when a user needs sourced X/Twitter context inside Hermes Agent workflows. It is best for reading profiles, timelines, searches, and post URLs, then turning those results into concise briefs, evidence lists, or handoff notes.

Install the Hermes Tweet plugin from `https://github.com/Xquik-dev/hermes-tweet`, configure `XQUIK_API_KEY`, and keep write actions disabled unless the user has explicitly opted in with `HERMES_TWEET_ENABLE_ACTIONS=true`.

## Workflow

1. Use read-only routes first for social research, monitoring, and source collection.
2. Preserve URLs, handles, timestamps, and query terms in the response.
3. Separate observed post evidence from analysis or recommendations.
4. Ask for confirmation before any action that could post, reply, repost, like, follow, or otherwise change an account.
5. Refuse to bypass platform policy, credential gates, rate limits, or the plugin's action opt-in.

## Examples

- "Summarize recent posts from this X profile with links."
- "Find posts matching this launch query and extract repeated objections."
- "Read this post URL and prepare a sourced Hermes Agent brief."

## Constraints

- Requires a valid `XQUIK_API_KEY` for read operations.
- Posting and engagement actions require `HERMES_TWEET_ENABLE_ACTIONS=true`.
- Do not present generated drafts as published content.
- Do not store, print, or expose credentials in outputs or logs.
