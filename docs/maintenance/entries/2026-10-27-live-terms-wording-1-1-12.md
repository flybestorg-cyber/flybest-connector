# 2026-10-27 Skill/README 1.1.12: charge line from live terms, after-booking checks, ChatGPT bundles the Skill

- Record ID: 2026-10-27-live-terms-wording-1-1-12
- Date and time zone: 2026-10-27, America/Los_Angeles
- Related records: [2026-10-14-booking-wording-1-1-9](2026-10-14-booking-wording-1-1-9.md) (e-mail optional, two price-change cases), [2026-10-26-chatgpt-plugin-published](2026-10-26-chatgpt-plugin-published.md) (wrote the "Skills are for Claude" sentence), [2026-10-26-chatgpt-package-1-1-11](2026-10-26-chatgpt-package-1-1-11.md) (the ChatGPT package bundles this skill with one client-neutral line), [2026-10-07-hotel-skills-conversion](2026-10-07-hotel-skills-conversion.md) (post-booking verification wording). Service side: booking-service record `2026-10-27-review-fix-g6-tool-text` (same day).
- Affected files: `skills/flybest-hotels/SKILL.md` (sections 5 and the after-booking bullet), `README.md` (Use in ChatGPT, Connect → ChatGPT, the "Using another client" paragraph, Updating), `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.11 → 1.1.12). The ChatGPT package is not kept here; its changes are listed below.

## Problem and cause

A review of the service and its plugins (three reviewers, October 2026) found four public texts that no longer matched the live service:

1. **Deposit and non-refundable flags.** Since 2026-10-15 every hotel payment page shows the rate's live price, deposit and cancellation terms and books once the payer ticks them; `allow_deposit` / `allow_nonrefundable` are no longer needed. The skill still said the flags mean "this rate may be offered" and to "set them only for a rate whose terms you have told the user". The service's own "may charge the card at booking" line was also still keyed on those flags, so a deposit or prepaid rate linked without them did not carry that line. The service now reads it from the rate's live terms (service record above); the skill now says so and tells the assistant to pass that line on before sharing the link, and not to share a link whose payment terms were not returned until the advisor has verified them.
2. **After-booking checks.** The skill told the assistant to verify the total, currency, room/bed and cancellation terms with `my_trips` / `my_trip`. Those tools return the hotel and dates, status, hotel confirmation, reservation reference and the booked guests and rooms, not the total, room type or cancellation terms. A model following the old text could call facts "verified" that no tool returned.
3. **README: "the Skills are for Claude".** The ChatGPT plugin bundles this same `flybest-hotels` skill (record 2026-10-26-chatgpt-package-1-1-11). The README said the opposite in two places and suggested pasting the skill into ChatGPT.
4. **ChatGPT example prompt.** "Show my upcoming hotel bookings and the cancellation terms for each" promises terms that `my_trips` does not return; the only source of current terms is the cancellation preview, which is a separate, rate-limited step.

## Change and reason

- `SKILL.md` §5: the flag sentence now says the flags are not needed and are not consent; the link result states, from the live terms, whether the card may be charged at booking; say so before sharing the link; an unreturned payment term means the advisor verifies before the link is shared.
- `SKILL.md` after-booking bullet: names exactly what `my_trips` / `my_trip` show, compares those with the selected quote, and says the total and cancellation terms are the ones the payment page showed and the traveller accepted, rather than calling them re-checked. The label-missing-details sentence stays.
- `README.md`: the ChatGPT plugin bundles the same skill; a skill change reaches ChatGPT with the next reviewed plugin version, so the ChatGPT copy can lag one version; the paste advice is limited to other clients; Updating says the ChatGPT skill changes with a new reviewed version.
- Version 1.1.12 in both manifests, because installed Claude plugins only receive changed skill text with a new version.

Kept: the payment page remains the only place for card details and consent; the two price-change cases, the ten-minute page window and the unknown-outcome rules are unchanged.

## User experience and compatibility

Travellers are no longer asked about flags, are told before receiving a link when the rate may charge at booking, and are not told that the booking list re-confirmed a total or cancellation terms it does not show. Existing installs keep 1.1.11 until they update; the server's own instructions and tool descriptions carry the same change for tools-only and ChatGPT connections once the service release is live.

## ChatGPT package (prepared, not built or uploaded)

The next ChatGPT package needs, starting from the approved 1.1.11 package:

- `skills/flybest-hotels/SKILL.md` = this repository's 1.1.12 skill with the same single client-neutral edit as before ("complete Claude's" → "complete the current client's"); `references/quote-integrity.md` is unchanged.
- `.codex-plugin/plugin.json`: `version` 1.1.12; `interface.defaultPrompt[2]` "Show my upcoming hotel bookings and their confirmation numbers"; new `publication.release_notes` describing the two skill changes. Description, long description, URLs, icon and MCP configuration unchanged.

Building the ZIP, uploading the draft and submitting it for review are left to the owner.

## Verification

- Service test `tests/test_public_contract_repair_2026_10_03.py` pins the manifest version (now 1.1.12) and that the skill names exactly the eight public tools; the service's new test file checks the README and skill sentences above (see the service record for counts).
- Manual read of the four changed passages; JSON manifests parse.

## Version and release status

- Related commit: see this record's Git commit (branch `fix/r27b-g6-tool-text`).
- GitHub push status: local commit only, not pushed.
- Published plugin versions: Claude directory and GitHub marketplace still 1.1.11; ChatGPT package unchanged.
- Restart: not applicable (documentation and skill only).

## Remaining limits

The skill can only describe what the tools return; it cannot make a client relay the charge line. The ChatGPT copy stays at its published version until the owner submits a new package and OpenAI approves it.
