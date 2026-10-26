# 2026-10-26 ChatGPT plugin package 1.1.11 (draft built from the published 1.1.8 package)

- Record ID: 2026-10-26-chatgpt-package-1-1-11
- Date and time zone: 2026-10-26, America/Los_Angeles
- Related records: [2026-10-14-booking-wording-1-1-9](2026-10-14-booking-wording-1-1-9.md) and the 1.1.10 / 1.1.11 records; the ChatGPT link records of the same day.
- Affected files in this repository: this record only. The ChatGPT package itself is not kept here.

## Problem and cause

The ChatGPT plugin went live with package version 1.1.8. Its bundled skill was this repository's 1.1.7 skill (one line changed, see below), so ChatGPT users did not get the 1.1.8 loyalty wording, the 1.1.9 payment-page wording, the 1.1.10 search-first behaviour or the 1.1.11 Marriott member-rate note. Updating skills or listing data on ChatGPT needs a new package version and a review; the MCP tool definitions and server instructions follow the live server through OpenAI's continuous review and need no new version.

The ChatGPT package uses OpenAI's Codex format (`.codex-plugin/plugin.json`, `.mcp.json`, `assets/icon.png`, `skills/`), not this repository's `.claude-plugin` layout, so it cannot be built from this repository alone.

## Change and reason

Starting from the published 1.1.8 release ZIP (downloaded by the owner from the portal):

- `skills/flybest-hotels/SKILL.md` replaced with this repository's 1.1.11 skill, with the same single client-neutral edit the 1.1.8 package carried: "complete Claude's" became "complete the current client's" (the only Claude-specific sentence). `references/quote-integrity.md` was already identical.
- `.codex-plugin/plugin.json`: `version` 1.1.8 → 1.1.11 and new `publication.release_notes`. Listing text, URLs, icon and the MCP configuration are unchanged.

## Version and release status

- 2026-10-26: uploaded as a draft (1.1.11) with "Create draft from ZIP". Metadata checks: no findings. Skill checks were still running when this record was written.
- Not submitted for review yet: submission waits for the owner's go-ahead. The published version stays 1.1.8 until a reviewed 1.1.11 is published.

## Remaining limits

The four changed MCP tools and the server instructions still show the definitions captured on 2026-10-09; continuous review has not reported a finished scan since the scanner reconnected on 2026-10-26.

## Review receipt — 2026-10-26

Skill checks passed (no findings on metadata or skills). With the owner's explicit go-ahead the draft was submitted for review at about 20:35 UTC, the six standard attestations ticked on the owner's confirmation, and a private note told the reviewers that this version changes only the bundled skill while the MCP updates are in continuous review. The portal showed "1.1.11 · Approved" and "Ready to publish" within minutes. Publishing is left to the owner; the live version stays 1.1.8 until then.
