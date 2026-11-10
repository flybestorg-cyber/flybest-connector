# 2026-11-09 Skill 1.1.19: a chat signed in by link gives the confirmation e-mail once

- Record ID: 2026-11-09-chat-link-email-1-1-19
- Date and time zone: 2026-11-09, America/Los_Angeles
- Related records: [2026-11-05-chat-signin-1-1-16](2026-11-05-chat-signin-1-1-16.md), [2026-11-05-signin-connect-hint-1-1-17](2026-11-05-signin-connect-hint-1-1-17.md); service side: sabre-booking record `2026-11-09-review-fix-chat-signin-email` (review finding L5, with TP-02).
- Affected files: `skills/flybest-hotels/SKILL.md` (booking confirmation bullet), `README.md` ("How booking works" step 1), `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.18 → 1.1.19).

## Problem and cause

The skill and README said the payment page is filled in with the address the traveller signed up with. Since the service release of 2026-11-09 that is true only for a connection made in the app's connector settings. A chat signed in through a one-time link no longer uses the signer's address as the default: the link can be forwarded, and the chat holder could read the signer's full address on a payment page the chat created (review 2026-11-09, finding L5). Such a chat now gets a refusal before anything is created when it asks for a payment page without an e-mail.

## Change and reason

- SKILL.md: the confirmation bullet separates the two cases. Connected in settings: the sign-up address is the default, pass `email` only for a different one. Signed in by link: ask once for the guest's e-mail and pass it; without it no payment page is made.
- README.md: step 1 of "How booking works" says the same in the traveller's words.
- Nothing else in the skill changes. The ChatGPT package is not affected (ChatGPT always connects through its own settings) and is not resubmitted.

## Customer experience and compatibility

In Claude Code or Codex chats signed in by link, the assistant asks for the confirmation e-mail once per booking. Connections made in claude.ai or ChatGPT behave as before. An older skill (1.1.18) still works: the tool's refusal itself says an e-mail is needed.

## Verification

Service side: sabre-booking `tests/test_review_fix_chat_signin_email_2026_11_09.py` (refusal for a link session with no e-mail, mint with an explicit one, OAuth default unchanged) and a second-model review (ship). Plugin side: `claude plugin validate` and the service's contract test that pins the plugin version (bumped to 1.1.19 in the same change). Not verified: a real model following the new wording in a live Claude Code chat.

## Release status

- Push and directory receipt: appended after release.

## Remaining limits

- The Claude directory may hold a new version for manual review (policy notice on earlier versions, see 2026-11-05 records).
