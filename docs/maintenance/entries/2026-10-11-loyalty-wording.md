# 2026-10-11 Loyalty wording restored, benefit-lookup status lines, install link wording (1.1.8)

- Record ID: 2026-10-11-loyalty-wording
- Date and time zone: 2026-10-11, America/Los_Angeles
- Related records: [2026-10-07-hotel-skills-conversion](2026-10-07-hotel-skills-conversion.md), [2026-10-08-public-hotel-skill-refresh](2026-10-08-public-hotel-skill-refresh.md). Server-side counterparts are recorded in the private booking-service repository under the same date.
- Affected files: `README.md`, `skills/flybest-hotels/SKILL.md`, `.claude-plugin/plugin.json`, `lhm.plugin.json`.

## Problem and cause

- **Loyalty wording.** The owner's long-standing statement, based on real bookings, is that points and elite nights are credited as usual through the advisor channel, and that status benefits apply on top of the partner benefits. Versions 1.1.6 and 1.1.7 replaced it with "points, elite-night credit and status benefits depend on the selected rate … not guaranteed for every rate" in the skill and the README paragraph. The README comparison table, the payment page and the booking tool description still said the opposite, so a traveller could read both versions.
- **Benefit-lookup status.** The skill told the assistant to tell an unchecked negotiated row apart from a failed lookup, but the tool output printed no per-row status for either case.
- **Install link.** The install link points to a plugin page that requires sign-in. The README presented it as the first step.

## Change and reason

- **Loyalty.** "Points and elite nights are credited as usual, and status benefits apply on top of the partner benefits" now appears in the README paragraph, both skill passages and the listing description. Member *rates* are still described as never guaranteed until a search with the traveller's number returns one; that is a separate question and is unchanged.
- **Benefit-lookup status.** The skill now quotes the two per-row status lines the service prints from this release on:
  - "benefits not checked — outside the lookup shortlist";
  - "benefit lookup timed out — … can be retried".
  The skill also says that neither line means "no benefits".
- **Install link.** The README now leads with Customize → Plugins → search FlyBest and labels the direct page link "sign-in required".
- **Version.** 1.1.8 in both manifests. The MCP endpoint and the tool set are unchanged.

## User experience and compatibility

Travellers see one consistent loyalty statement. Brands without a points programme are still described as giving benefits, not points. Installed plugins need the 1.1.8 skill; connector-only clients are unaffected.

## Verification

JSON manifests parse; the two plugin versions match; no internal paths, secrets or customer data were added. The quoted status lines match the server rendering shipped in the same-day booking-service release (verified against its tests before this push).

## Version and release status

- Commit: see the Git commit containing this record.
- Push and directory status: appended after publication.

## Remaining limits

Directory re-indexing and installed-client updates happen on the directory side and are not proven by this record.
