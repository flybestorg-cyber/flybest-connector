# 2026-11-10 Skill 1.1.20: the trip list covers the current sign-in

- Record ID: 2026-11-10-trip-list-scope-1-1-20
- Date and time zone: 2026-11-10, America/Los_Angeles
- Related records: [2026-11-09-chat-link-email-1-1-19](2026-11-09-chat-link-email-1-1-19.md), [2026-11-05-chat-signin-1-1-16](2026-11-05-chat-signin-1-1-16.md); service side: sabre-booking records `2026-11-09-signin-cap-and-chat-scope` and `2026-11-10-review-fix-trip-scope` (review finding TP-01).
- Affected files: `skills/flybest-hotels/SKILL.md` (section 6, first bullet), `README.md` (comparison table row "After booking"; "Why book through FlyBest" closing paragraph), `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.19 → 1.1.20).

## Problem and cause

The skill said "`my_trips` lists only this user's bookings" and the README said "see and cancel your own bookings". Since chat sign-in (service release 2026-11-05) each chat signed in with a one-time link is its own trip owner: a booking made in one chat is not listed in another chat or under a connection made in the app's settings, even with the same e-mail address. An empty list could be read as "the booking did not go through" (review 2026-11-09, finding TP-01).

## Change and reason

- SKILL.md section 6: the list covers the bookings made under the current sign-in — a connection's own, or, in a link-signed chat, only what was booked in that chat since the sign-in. A booking missing from the list is not proof that it does not exist or was cancelled; pass on who the result says can check it, and do not book again on the strength of an empty list.
- README.md: the two sentences that promised "your own bookings" now say "under the same sign-in", and name jay@flybest.org for a booking made elsewhere.
- The wording mirrors the service's tool descriptions and results (sabre-booking record `2026-11-10-review-fix-trip-scope`). Bookings are not merged by e-mail; that isolation is deliberate.

## Customer experience and compatibility

No behaviour change in the plugin itself. With the service release of 2026-11-10 the tool results say the same thing, so an older skill (1.1.19) still works; the new text keeps the model from concluding "not booked" before the result is read. The ChatGPT package is not affected (ChatGPT connects through its own settings, one sign-in) and is not resubmitted.

## Verification

Service side: sabre-booking `tests/test_review_fix_trip_scope_2026_11_10.py` and a second-model review (ship). Plugin side: `claude plugin validate`. Not verified: a real model following the new wording in a live chat.

## Release status

- Service release: sabre-booking `d51f6a1`, live 2026-11-10 08:06 PST (the tool descriptions and results with the same wording).
- Pushed to GitHub `main` on 2026-11-10 after the service release. ChatGPT package unchanged (1.1.17). Whether the Claude directory serves 1.1.20 was not checked at push time.

## Remaining limits

- After an app restart the same visible chat is a new sign-in and no longer lists what it booked before (service record `2026-11-09-signin-cap-and-chat-scope`).
- The Claude directory may hold a new version for manual review (policy notice on earlier versions, see 2026-11-05 records).
- Claude directory, checked 2026-11-10 about 08:20 PST: 1.1.20 (`6d2855f`) was picked up within minutes and its scan passed, but it is "held by directory policy, with Anthropic" like 1.1.15–1.1.19 (rules "Uses a credential from the user's machine" on `.claude-plugin/plugin.json` and "Update adds credential forward"). The live version is still 1.1.14 (`aa93765`). The ticket opened with the directory team on 2026-11-06 (#153092987) has had no answer beyond the automatic receipt.

