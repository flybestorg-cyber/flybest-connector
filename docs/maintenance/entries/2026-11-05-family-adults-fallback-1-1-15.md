# 2026-11-05 Skill 1.1.15: adults' prices when no rate verifies the family

- Record ID: 2026-11-05-family-adults-fallback-1-1-15
- Date and time zone: 2026-11-05, America/Los_Angeles
- Related records: [2026-11-02-signin-reminder-1-1-14](2026-11-02-signin-reminder-1-1-14.md); service side: sabre-booking record `2026-11-05-family-adults-fallback`.
- Affected files: `skills/flybest-hotels/SKILL.md` (section 4, the unverified-family bullet), `README.md` (the family example), `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.14 → 1.1.15).

## Problem and cause

A family asked for rates at two hotels whose supplier does not price children. Every lookup came back as an error and the traveller left with no price. The owner's rule (2026-11-05): when children's prices can be checked, use them; when they cannot, look up the adults' prices and have the traveller contact Jay.

## Change and reason

The service now does the adults' lookup itself when no rate verifies the family, and the result opens with a note that the prices exclude the children. Section 4 tells the assistant to present those prices as the adults' prices only, never as a family total, and to offer Jay's help for the stay with children. The verified family path, the request for each child's age, the adults-first option (explicit choice only) and the no-e-mail-without-request rule are unchanged. The README example says the same in one sentence.

## Customer experience and compatibility

Families at hotels that do not price children see the hotel's adult prices, clearly marked, and Jay's address, instead of an error. Older installed versions get the same server behaviour; their Skill text still offers Jay's help, which matches.

## Verification

- Text checked against the service output in the sabre-booking tests (`tests/test_family_adults_fallback_2026_11_05.py`) and the pinned version in `tests/test_public_contract_repair_2026_10_03.py`.
- Directory note (2026-11-05): the live 1.1.14 shows a directory policy hold from 2026-11-04, "Uses a credential from the user's machine" (rule MCP_FORWARDS_CREDENTIAL_ENV, flagged on `.claude-plugin/plugin.json`). The manifest has no credential or environment variable, only the HTTP MCP URL; 1.1.14 keeps serving. 1.1.15 may wait for a reviewer before going live.

## Release status

- Push and directory receipt: appended below after release.
- ChatGPT package: not resubmitted; needs the owner's go-ahead to publish (the server behaviour does not depend on it).
