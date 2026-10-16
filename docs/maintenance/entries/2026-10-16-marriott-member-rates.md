# 2026-10-16 Marriott Bonvoy member rates now come back (1.1.11)

- Record ID: 2026-10-16-marriott-member-rates
- Date and time zone: 2026-10-16, America/Los_Angeles
- Related records: [2026-10-11-loyalty-wording](2026-10-11-loyalty-wording.md) (points and status wording), [2026-10-14-search-first-draft](2026-10-14-search-first-draft.md) (1.1.10, membership asked with the first quotes for real dates), [2026-10-04-public-docs-live-contract](2026-10-04-public-docs-live-contract.md) (README states only what the connection returns). Server-side counterpart: the private booking-service repository, record `2026-10-16-marriott-y47` (same date), which adds the Marriott member-rate search and changes the server instructions and tool descriptions to the same wording.
- Affected files: `README.md` ("Member rates"), `skills/flybest-hotels/SKILL.md` ("Member rates"), `.claude-plugin/plugin.json`, `lhm.plugin.json`.

## Problem and cause

The README and the skill said Marriott member rates are not available through this connection, and told the assistant not to search a Marriott hotel again with the traveller's number. That was true when written: the member-rate code tried for Marriott returned nothing. On 2026-10-16 the owner had another Marriott member-rate code tested read-only. It returned Marriott's own member rates, marked members-only, at some Marriott properties (3 of 16 tried), about 2% under the same room's public rate, and those rates passed the reservation system's price check. The owner approved wiring it in and changing every text that said otherwise.

## Change and reason

- **Skill, "Member rates".** Marriott Bonvoy joins Hilton Honors, World of Hyatt, IHG One Rewards and I Prefer: its member rates are already in the rate list, marked members-only, at some Marriott hotels, not all (about 2% under the public rate where measured). At a Marriott hotel the assistant now searches again with the traveller's number before confirming a members-only rate, like the others. The "do not search again at Marriott" sentence is gone.
- **README, "Member rates".** Same facts in the traveller's words; Marriott Bonvoy added to the free programmes to join. "No member discount is guaranteed" stays.
- **Unchanged.** A members-only rate books only from a search made with the traveller's own number, and a rate found with a number books only with that number. Points and elite nights are credited as usual. Rates the reservation system returns without a member code are not shown as Marriott member rates (the service keeps only the coded ones).
- **Version.** 1.1.11 in both manifests. The MCP endpoint and the eight public tools are unchanged.

## User experience and compatibility

At a Marriott hotel the rate list may now include rows marked members-only; the assistant asks for the Bonvoy number with the first quotes and searches again with it before booking such a row. Where none come back, nothing changes. Installed plugins need the 1.1.11 skill; connector-only clients get the matching server instructions directly once the service release is live.

## Verification

`claude plugin validate .` passes (one existing warning: the root CLAUDE.md is maintainer context, not plugin context). JSON manifests parse and both versions read 1.1.11; no internal paths, agency codes, secrets or customer data were added. The wording matches the server instructions and the public `sabre_hotel_rates_coded` description in the same-day booking-service change, whose tests check the server side and this checkout's manifests (when it sits beside the service checkout).

## Version and release status

- Commit: see the Git commit containing this record.
- Push status: local commit only, not pushed (the owner's maintainer pushes together with the service release).
- Directory status: not published; appended after publication.

## Remaining limits

Marriott member rates came back at a minority of the properties tried, all in the US; luxury Marriott brands tried returned none. A real member's number was not tested. Directory re-indexing and installed-client updates happen on the directory side and are not proven by this record.
