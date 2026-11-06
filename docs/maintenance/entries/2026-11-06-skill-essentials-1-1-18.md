# 2026-11-06 Skill 1.1.18: essentials first, so they survive a long chat; maintainer notes out of the plugin root

- Record ID: 2026-11-06-skill-essentials-1-1-18
- Date and time zone: 2026-11-06, America/Los_Angeles
- Related records: [2026-11-05-signin-connect-hint-1-1-17](2026-11-05-signin-connect-hint-1-1-17.md); service side: sabre-booking record `2026-11-06-claude-code-mcp-limits` (server instructions core block, tool hints).
- Affected files: `skills/flybest-hotels/SKILL.md` (new "Essentials" section), `CLAUDE.md` → `.claude/CLAUDE.md`, `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.17 → 1.1.18).

## Problem and cause

The owner asked to apply what Claude Code's documentation says about skills and MCP servers. Two points apply to this plugin:

- When a long conversation is compacted, Claude Code re-attaches only about the first 5,000 tokens of an invoked skill. This skill is about 9,000 tokens; children (§4), booking (§5), cancellations (§6) and "What you must not do" (§8) sit beyond that, so a long hotel conversation could continue without them.
- The directory's validation warns that a `CLAUDE.md` at the plugin root is not loaded. That file holds maintainer instructions for this repository, not traveller instructions.

## Change and reason

- New "Essentials" section right after the sign-in section (it ends at about 5,800 characters of the body): prices only from tool results, search first, how to quote a rate, the traveller note and membership question, children and the adults-only fallback, booking and the payment page, never handling card numbers, changed prices, cancellation consent, unclear outcomes, hotels only. It restates the numbered sections in fewer words; the numbered sections are unchanged and still give the detail.
- `CLAUDE.md` moved to `.claude/CLAUDE.md` (imports now `@../AGENTS.md`, `@../docs/maintenance/README.md`); Claude Code still loads it for maintainers working in this repository, and the plugin root no longer carries it.
- The service now puts a short core block at the start of its instructions for the same reason (Claude Code reads only their first 4,096 characters) and lists the hotel search and rate tools upfront; see the service record.

## Customer experience and compatibility

No tool, parameter or booking behaviour changes. In long Claude Code conversations the assistant keeps the booking, children and card-number rules after compaction.

## Verification

- `claude plugin validate .`: passed with no warnings (before: the CLAUDE.md warning).
- Essentials checked against the numbered sections and the service's public instructions in review. Round 1 found that the booking bullet let a link be shared when its payment terms were not returned; it now says to disclose a possible charge at booking before sharing, and not to share the link until the advisor has verified missing payment terms (as §5 says).
- Service contract test (sabre-booking `tests/test_public_contract_repair_2026_10_03.py`, pins 1.1.18) run against this checkout: passed.

## Release status

- Pushed to the tracked branch on the owner's instruction (2026-11-06: "不要hold back了，直接改") although the directory still holds 1.1.15–1.1.17 for review; receipt appended after release.
