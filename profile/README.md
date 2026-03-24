# Oxvault

**The vault that guards your AI tools.**

Oxvault is an open-source MCP (Model Context Protocol) security platform. We protect the connection layer between AI agents and the tools they use.

## The Problem

MCP is becoming the standard protocol for connecting AI agents (Claude, GPT, Copilot, Cursor) to external tools. But the ecosystem is growing faster than its security:

- **66% of MCP servers** have security vulnerabilities
- **53%** use hardcoded API keys instead of OAuth
- **30+ CVEs** filed in just 60 days
- Real-world incidents at named companies - data breaches, supply chain attacks, nation-state exploitation

There is no comprehensive security tooling for this attack surface. Until now.

## What We Build

### Scanner - catch vulnerabilities before installation
```bash
$ oxvault scan @company/mcp-server

  CRITICAL  mcp-tool-poisoning (E003)
  Tool "calculator" contains hidden exfiltration instruction
  Found: <IMPORTANT> tag with credential theft payload

  HIGH  mcp-cmd-injection
  server.py:19 - os.popen(f"curl {user_input}")
  Tool parameter passed directly to shell

  2 CRITICAL · 1 HIGH · 0 WARNING
```

### Gateway - enforce policy at runtime
```bash
$ oxvault wrap npx -y @company/mcp-server
# Every tool call inspected. Injection blocked. PII redacted. Full audit trail.
```

### Trust Registry - verify before you deploy
```
Trust score: 87/100 · Last scanned: 2h ago · CVEs: 0 · Auth: OAuth 2.1 ✓
```

## Why Oxvault

| | Existing Tools | Oxvault |
|---|---|---|
| Static scanning | Fragmented (5+ tools, each partial) | Unified scanner - source code + descriptions + credentials + deps |
| Runtime protection | HTTP only | **HTTP + stdio** (the only gateway that covers local MCP servers) |
| Credential hygiene | Nobody checks this | **Core feature** - enforces OAuth over static keys |
| Rug pull detection | Basic hash check | Continuous drift monitoring with automated alerts |
| Trust registry | Doesn't exist | Security-scored server catalog with enterprise policy enforcement |
| CI/CD integration | Minimal | SARIF output, GitHub Actions, GitLab CI |

## Tech Stack

- **Scanner & Gateway:** Go - single binary, zero dependencies
- **Detection rules:** Semgrep + YARA + custom pattern matching
- **Dashboard:** Vue 3 + Nuxt
- **Registry API:** Go + PostgreSQL

## Get Involved

We're building in the open. Star the repos, open issues, submit PRs.

---

*Securing the AI tool layer. Open source. No blind spots.*
