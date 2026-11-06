# 2026-11-05 Skill 1.1.17: always name the lasting Connect option; prefer a signed-in FlyBest connection

- Record ID: 2026-11-05-signin-connect-hint-1-1-17
- Date and time zone: 2026-11-05, America/Los_Angeles
- Related records: [2026-11-05-chat-signin-1-1-16](2026-11-05-chat-signin-1-1-16.md); service side: sabre-booking record `2026-11-05-signin-connect-hint`.
- Affected files: `skills/flybest-hotels/SKILL.md` (sign-in bullets), `README.md` (Claude Code first use), `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.16 → 1.1.17).

## Problem and cause

The owner asked whether travellers are sure to be told to connect FlyBest once (so every chat is signed in) rather than signing in per chat. The in-chat link only signs in one chat. A second gap: someone who already connected FlyBest in Claude's settings and also has the plugin sees two sets of FlyBest tools in Claude Code-based apps; if the assistant picked the plugin's set, it would pass on a sign-in link although the person is signed in.

## Change and reason

- The sign-in bullet now says, in Claude apps signed in with a Claude account, to always add the lasting option (Customize → Connectors → FlyBest → Connect, same e-mail) when passing on a link. It is scoped (review): that connection does not sign in Codex or a Claude Code session that uses an API key; there each chat signs in with its link. README says the same.
- New bullet: with two sets of FlyBest tools, use the set that returns results; no sign-in link while the other set is signed in.
- The service's tool result, public instructions and the sign-in page say the same (service record).

## Customer experience and compatibility

Travellers see the lasting option in the chat, on the sign-in page before the code and on the success page. People already connected are not asked to sign in again. No tool or booking behaviour changes.

## Verification

Real Claude Code (Haiku and Sonnet) against production on 2026-11-05, asked in Chinese for Paris hotels without any instruction to quote: both replies included the sign-in link and the Customize → Connectors → FlyBest → Connect option. Service tests in the sabre-booking record.

## Release status

- Push and directory receipt: appended after release.
