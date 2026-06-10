# Contributing

Thanks for helping builders ship into Korea.

## What belongs here

A resource belongs on this list if a foreign or AI-assisted builder can **plug it in** to ship a product into the Korean market: an API, SDK, MCP server, extension, plugin, or platform service. This is a builder's stack, not a directory of every Korean company.

## What does not belong

- Resources with no developer surface (marketing pages, news).
- Generic global tools that are not Korea-specific (put those on a general awesome list).
- Anything you have not verified actually works.

## Entry format

Add your entry to the right section's table:

```
| [Name](https://official-url) | One-line, what a builder gets | 🌐 | 🔑 | 🛂 | 💰 | 🤖 |
```

Fill the five signals honestly using the [Legend](README.md#legend):

- 🌐 **Docs**: `EN`, `KO`, or `EN~` (partial)
- 🔑 **Auth**: `key`, `oauth`, or `cert` (공동인증서 required)
- 🛂 **Foreigner access**: ✅ / ⚠️ / ❌ with a short reason if ⚠️ or ❌. This is about a Korean *presence* (a business entity or residency via an ARC / 외국인등록증), not nationality. A foreign resident with an ARC can complete 본인인증 and get a 공동인증서, so never rate something ❌ just because it needs those. Reserve ❌ for a confirmed entity/residency/citizenship block (true citizenship-only cases are rare).
- 💰 **Cost**: `free`, `freemium`, `paid`
- 🤖 **AI-ready**: `MCP`, `SDK`, or `REST`

## The one hard rule

**Do not guess the foreigner-access (🛂) rating.** It is the whole value of this list. If you have not personally tried to sign up from outside Korea, or confirmed it from official docs, mark the entry `⚠️ unverified` and say so in your PR. A wrong ✅ wastes a builder's day.

## Korean terms

Lead with the English term, put the Korean in parentheses on first mention: `identity verification (본인인증)`. Most readers do not read Korean.
