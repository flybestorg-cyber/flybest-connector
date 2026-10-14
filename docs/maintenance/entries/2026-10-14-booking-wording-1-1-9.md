# 2026-10-14 Booking wording: optional e-mail, the payment-page window, two "price changed" cases (1.1.9)

- Record ID: 2026-10-14-booking-wording-1-1-9
- Date and time zone: 2026-10-14, America/Los_Angeles
- Related records: [2026-10-08-public-hotel-skill-refresh](2026-10-08-public-hotel-skill-refresh.md), [2026-10-11-loyalty-wording](2026-10-11-loyalty-wording.md), [2026-10-14-readme-updating](2026-10-14-readme-updating.md). Server-side counterparts are recorded in the private booking-service repository under the same date (public link e-mail and wording, payment-page window, offer refusal alerts).
- Affected files: `skills/flybest-hotels/SKILL.md`, `README.md`, `.claude-plugin/plugin.json`, `lhm.plugin.json`.

## Problem and cause

- **E-mail asked twice.** Travellers sign in with an e-mail code, yet the skill told the assistant to collect an e-mail before creating the payment page, and the public tool schema required one. The payment page already has a confirmation-address field the payer can change.
- **"Price changed" had one case.** The skill said a changed price is shown on the existing payment page for the traveller to agree again. When the payment-page request itself is refused (`RATE_CHANGED_BEFORE_BOOKING`, `RATE_UNAVAILABLE`, `PRICE_CHECK_UNAVAILABLE`, `OCCUPANCY_MISMATCH`), no page exists, so following that sentence sent the traveller looking for a page that was never made.
- **The page window was easy to miss.** A payment page is open for about ten minutes. The skill said to pass on "the returned expiry" without saying when to create the page or what happens after it closes.

## Change and reason

- **E-mail.** Optional. Without one, the service fills in the address the traveller signed up with, and the payer confirms or changes it on the page. The assistant passes `email` only when the traveller gives one for the confirmation.
- **Two cases.** (1) A page exists and shows a changed total, deposit or cancellation penalty for the same room and stay: the traveller agrees again on that page. (2) No page was created: nothing is held; the assistant explains the change the result lists, gets a fresh rate row, confirms it with the traveller and creates the page from that row. `PRICE_CHECK_UNAVAILABLE` alone may be retried with the same row after a short wait. A different room, date or currency still needs a newly selected quote.
- **Window.** The page is open for about ten minutes and the tool result now gives the closing time. Create the page when the traveller is ready to pay and give the time with the link. If it closes unpaid, nothing was booked or charged; get the current rate again and create a new page straight away.
- **README.** "How booking works" says the same three things in the traveller's words.
- **Version.** 1.1.9 in both manifests. The MCP endpoint and the tool set are unchanged; the `sabre_hotel_card_link` schema no longer lists `email` as required for public connections.

## User experience and compatibility

After choosing a room, the traveller confirms the room, total, terms and name as on ID and gets the link without being asked for an e-mail again. Installed plugins need the 1.1.9 skill; connector-only clients get the matching server instructions directly. A client that cached the old tool schema still works (it simply sends an e-mail).

## Verification

JSON manifests parse and both versions match; no internal paths, secrets or customer data were added. The wording matches the server instructions and tool results in the same-day booking-service change, checked against its tests.

## Version and release status

- Commit: see the Git commit containing this record.
- Push and directory status: appended after publication.

## Remaining limits

Directory re-indexing and installed-client updates happen on the directory side and are not proven by this record. The ten-minute window itself is unchanged.

## Publication receipt — 2026-10-14

The matching booking-service release went live the same day at 21:50 UTC (public schema without a required e-mail, closing time in the payment-link result, the two changed-price cases in the server instructions). This commit is pushed to GitHub main; directory refresh and installed-client uptake are not verified here.
