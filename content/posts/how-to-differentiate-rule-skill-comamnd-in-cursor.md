+++
date = '2026-03-18T09:34:25+07:00'
draft = true
title = 'How to Differentiate Rule Skill Comamnd in Cursor'
tags = ["cursor", "editor", "ai"]
categories = ["Tools"]
+++

Rules apply to the system prompt. There are 4 types: Always Apply (always), Apply Intelligently (the agent decides), Apply to Specific Files (by glob patterns), and Apply Manually (via @mention). They’re stored in .cursor/rules/.

Commands run via / in chat. Important note: per agent best practices, the agent can use commands autonomously, so they’re not only for manual use. They’re stored in .cursor/commands/.

Skills (nightly only) are portable knowledge packages for the agent. The agent decides when they’re relevant, or you can invoke them via /. Unlike Commands, this is an open standard (agentskills.io) and works cross platform. They’re stored in .cursor/skills/ as SKILL.md.

Subagents (nightly only) are separate AI assistants with isolated context for complex tasks. They can run in parallel or in the background. They’re stored in .cursor/agents/.

When to use what:

Rules: permanent instructions like code style and architecture standards (short, under 500 lines)
Commands: repeatable workflows (code review, create PR, security audit)
Skills: specialized domain knowledge for the agent if you’re on nightly
Subagents: complex multi step tasks that need isolated context or parallel work (nightly)
Docs:

Rules | Cursor Docs
Commands | Cursor Docs
Agent Skills | Cursor Docs
Subagents | Cursor Docs
If you’re on the stable channel, only Rules and Commands are available. Skills and Subagents require nightly.
