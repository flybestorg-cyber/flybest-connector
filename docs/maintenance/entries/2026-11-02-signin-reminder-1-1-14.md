# 2026-11-02 Skill 1.1.14: remind every time until FlyBest is signed in; no prices before sign-in

- Record ID: 2026-11-02-signin-reminder-1-1-14
- Date and time zone: 2026-11-02, America/Los_Angeles
- Related records: [2026-11-02-plugin-connector-signin-1-1-13](2026-11-02-plugin-connector-signin-1-1-13.md) (same day: cause and the first fix), [2026-10-27-live-terms-wording-1-1-12](2026-10-27-live-terms-wording-1-1-12.md).
- Affected files: `skills/flybest-hotels/SKILL.md` (description, new section "Not signed in yet: remind every time" after the introduction, section 9 now points to it), `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.13 → 1.1.14).

## Problem and cause

1.1.13 told users how to connect FlyBest only once Claude noticed, inside section 9, that the tools were missing. The owner's requirement (2026-11-02): everyone who has the plugin but has not signed in must be reminded to sign in, every time, and hotel prices must stay sign-in only. The Skill is available wherever the plugin is installed, signed in or not; its description is visible to Claude in every conversation, so the description and the opening of the Skill are the places that reach those users.

## Change and reason

- Description: the Skill also applies to trip planning that needs a place to stay, and says that, while the FlyBest tools are unavailable, every hotel or travel reply starts with a reminder to connect FlyBest and sign in (free, e-mail code).
- New section right after the introduction: check whether the tools are available; if not, open every hotel or travel reply with the reminder (Customize → Connectors → Connect and the e-mail code; the + → Connectors switch if already connected; `/mcp` for `plugin:flybest-hotels:flybest` in Claude Code; then a new chat), in the user's language. Until then no hotel prices of any kind (no ranges, typical, market or reference prices, from memory or web search), no availability, no benefits; general information about areas and hotels is allowed. If FlyBest is connected and switched on and the tools are still missing, offer the advisor contact. Conversations not about hotels or travel get no reminder, so unrelated chats are not affected.
- Section 9's missing-tools bullet now points to that section instead of repeating it.

No tool, server instruction, sign-in or booking behaviour changes.

## Customer experience and compatibility

A user who added the plugin but never signed in is reminded at the start of every hotel or travel reply, gets no prices until signed in, and is told exactly where to connect. Signed-in users see no difference. Installed plugins need 1.1.14.

## Verification

Claude Code (current release) in a fresh profile with this plugin loaded from the working copy and FlyBest not signed in, synthetic prompts:
- A hotel request (English, Hyatt, specific dates): the reply opened with the reminder and gave no rates.
- A first run of a Chinese "where to stay and roughly how much" request opened with the reminder but listed reference price ranges; the rule was tightened to "no hotel prices of any kind". Re-run: reminder first, no prices, area advice only.
- A single-hotel price question and a business-trip hotel question: reminder first, no prices.
- An unrelated coding question: no reminder.
`claude plugin validate`: passed with the known warnings (root CLAUDE.md is maintainer context; privacy URL taken from README).

## Version and release status

- Commit: see this record's Git commit. GitHub push and Claude directory receipt to be appended; the directory auto-publishes versions that pass its scan.
- No service restart or backend deployment.

## Remaining limits

The reminder appears only when the Skill is consulted, which the description now asks for in every hotel or travel conversation; Claude can still occasionally skip a Skill. The sign-in itself is still started by the user; Claude apps decide whether to prompt for it.
