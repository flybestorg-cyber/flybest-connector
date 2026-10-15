# 2026-10-14 Search first, ask later — skill side (1.1.10, draft, not published)

- Record ID: 2026-10-14-search-first-draft
- Date and time zone: 2026-10-14, America/Los_Angeles
- Status: **draft, not published; held with sabre-booking `draft/public-search-first-2026-10-14`.** Local branch and commit only: not pushed, not merged, not published in the Claude directory. It ships only together with that server draft, after the owner approves both.
- Related records consulted: [2026-10-07-hotel-skills-conversion](2026-10-07-hotel-skills-conversion.md) (priced recommendations in the same answer), [2026-10-08-public-hotel-skill-refresh](2026-10-08-public-hotel-skill-refresh.md), [2026-10-11-loyalty-wording](2026-10-11-loyalty-wording.md) (membership wording), [2026-10-14-booking-wording-1-1-9](2026-10-14-booking-wording-1-1-9.md) (current skill and versions). Server-side counterpart: the private booking-service record `2026-10-14-public-search-first` on the branch named above (public profile only: dates optional on `sabre_hotel_search`, sample-dates search, rewritten server instructions).
- Affected files: `skills/flybest-hotels/SKILL.md`, `.claude-plugin/plugin.json`, `lhm.plugin.json`. `server.json` (MCP Registry entry, 1.0.2) is unchanged: the endpoint and the tool set are the same.

## Owner's decision — 2026-10-14

The owner decided that the search-first change ships only after the OpenAI app review passes. Until then this branch stays a local commit: not pushed, not published in the Claude directory. The server branch of the same name is held the same way. At release, both branches are rebased onto their then-current main lines, the offline checks are run again, and they go out together (server first, then this plugin).

## Problem and cause

Travellers connect the hotel connector but rarely get a search. In offline tests against the public tool surface, casual first questions ("hotels in Tokyo", "东京有什么好酒店推荐？" and four others, two models, 18 runs) never called the search tool; every answer was a questionnaire of four to six items. Questions that already carried dates and a party searched straight away. Two causes on our side: the public search required check-in and check-out dates, and the instructions said to collect dates, party, beds, plans and membership before searching.

The server draft removes both causes for public connections. This skill still said "If check-in/check-out dates or the party … are missing, ask for the missing essentials together in one short message", "Never guess stay dates" and "Ask about membership near the start". A Claude user with the plugin installed would read the opposite of the server instructions.

## Change and reason

The skill now gives the same behaviour as the server draft, in the same words where practical:

- **Search first, ask later** (new first bullet of "Turn hotel interest into a priced choice"). Any question about hotels, where to stay, hotel prices or availability calls `sabre_hotel_search` in the same turn, before any question and instead of an answer from general knowledge or web search. Without dates the public search uses sample dates and says so on its first line ("Sample dates: …"). If a connection's search still requires dates or refuses a search for missing dates (an invited connection, or a client with the old schema cached), the assistant asks for the dates and party in one line instead.
- **Sample-dates answer.** One plain sentence that these are example prices for sample dates; the hotels, partner-benefit properties first; then exactly one line asking for the stay dates and party (adults, children's ages, rooms) and nothing else. Bed preference, plan firmness and membership wait for the first quotes for the traveller's own dates. Sample dates are never rate-checked, presented as the traveller's total or used for a payment page.
- **Consistency edits, needed so the skill does not contradict itself.** The "include live formal quotes in that same answer" bullet now applies once the traveller's own dates and party are known; the "ask for the missing essentials together" bullet is replaced (its remainder kept: quote without another permission step, label beds); the closing "which hotel and rate" line notes that a sample-dates answer asks its dates-and-party line instead; §1 "Never guess stay dates" adds that a search without dates is not a guess (the service picks and labels the sample dates) and the assistant never picks dates itself; Member rates now asks about membership with the first quotes for the traveller's own dates, never in a sample-dates answer. Everything else is unchanged.
- **Description.** Adds when to use the skill (any question about hotels, where to stay, prices or availability), why (live bookable rates and partner benefits that general knowledge and web search lack) and Chinese trigger words (酒店、住哪、订房、住宿推荐、房价). It stays short and avoids a YAML-breaking colon.
- **Version.** 1.1.10 in both plugin manifests.

Not adopted: keeping "ask first" in the skill and relying on the server instructions alone. Installed plugins load the skill as well, so the conflicting sentence would stay in front of the model.

## User experience and compatibility

- With the server draft live: a casual question gets hotels in the same turn, labelled as example prices for sample dates, followed by one line asking for dates and party. The next turn quotes the traveller's own dates as before, with bed, plans and membership asked in one line alongside those quotes.
- Without the server draft (or on a connection whose search still requires dates): the search-first bullet falls back to one line asking for dates and party, which is close to the old behaviour. This is why the two must ship together: publishing the skill alone would mostly fall back, and the server alone would leave plugin users reading the old "ask first" rule.
- Bookings, payment pages, cancellation and the loyalty wording are unchanged. Sample dates never reach a rate check, a quoted total or a payment page.

## Verification

- Wording compared line by line with the server draft's public instructions (search first, sample-dates answer, one-line dates-and-party question, bed/plans/membership with the first own-date quotes, sample dates never quoted or booked).
- Frontmatter parses as YAML; `name` unchanged; description under 1,024 characters.
- `claude plugin validate .` passes; JSON manifests parse and both plugin versions read 1.1.10.
- The booking-service's cross-repository contract checks (both manifests on the public endpoint, marketplace name, all eight public tool names in the skill, README install wording) pass against this branch when run by hand with the version expected as 1.1.10. That test cannot run in the draft's worktree without a test database, so the assertions were replicated read-only.
- No internal paths, secrets or customer data added.
- The behavioural tests (offline trigger test: 0/18 → 17/18 first-turn searches; second turn 12/12 asking only dates and party) were run on the server draft's tool surface and instructions, not on this skill text. A combined test with this skill loaded has not been run.

## Version and release status

- Commit: see the Git commit containing this record, on local branch `draft/public-search-first-2026-10-14`.
- GitHub push: **not pushed.** Claude directory: **not published.**
- Release order if approved: deploy the server draft first, then push this branch, then Publish in the Claude directory (claude.ai/directory/manage), then Refresh tools in a client and ask one casual question to check the first line and the follow-up question. Append a receipt here after publication.
- The OpenAI plugin review was in progress when this was drafted; this repository does not change the ChatGPT app definition.

## Remaining limits

- A model that cached the old search schema (dates required) keeps asking for dates until the client refreshes its tools.
- Invited (non-public) connections keep dates required on the server; for them the skill's fallback line applies.
- Sample dates fall on whatever weekday they land on; the result's first line already says they are examples.
- The booking-service contract test still pins the plugin version at 1.1.8 (already behind 1.1.9 on main; it only runs when a connector checkout sits beside the service checkout). When the two drafts are merged, that pin moves to 1.1.10 in the service repository.

## Review round 1 and fixes — 2026-10-15 (still a draft: not pushed, not published)

An independent model review of this branch and the server draft together returned "ready after fixes" with ten findings; all were confirmed against the text and the saved offline outputs. Correction to the statement above: the earlier "second turn 12/12 asking only dates and party" held only for bed, plans and membership. Re-read against the full contract, 2 of those 12 answers opened with the sample sentence and 7 of 12 ended by asking whether to book one of the sample-priced hotels.

Changes to `skills/flybest-hotels/SKILL.md`:

- **Sample-dates answer order.** Sample sentence → the result's booking note → hotels (partner-benefit properties first) → one line asking for stay dates and party. That is the only question; bed, plans, membership and which hotel to book wait for the first own-date quotes. The closing reminder is a statement ("Once your dates are quoted, I can set up a secure payment page here for the rate you choose."). A hotel picked from a sample answer still needs the traveller's own dates and party before any rate lookup; dates the traveller gives or confirms are theirs even if they match the sample.
- **Rate lookups are conditional.** The shortlist bullet and the "continue the rate lookup in this turn" bullet now apply once the traveller's own dates and party are known.
- **Remaining ask-first sentences.** A month without exact dates gets a sample-dates search first; children's ages are asked before quoting rates (after a sample search, in its one line); the priority question comes with the first own-date quotes.
- **Scope.** Search first covers finding hotels, recommendations, prices and availability; a question only about an identified property's facilities, photos or check-in times uses `sabre_hotel_content`, and existing bookings use `my_trips` / `my_trip`.

Verification (offline, the same prompts and models as before, nothing sent to the live service): with the matching server draft, 24 of 24 second-turn answers (12 with the server instructions only, 12 with this skill loaded as well) opened with the sample sentence, none asked whether to book, and in a third turn ("the Park Hyatt looks good") none fetched rates or created a payment page on the sample dates — each asked for the traveller's dates and party. A strict script passed 16 of 24 on every check; the 8 it failed were checked by hand and meet the contract (one dates-and-party line split by several question marks, a request phrased without a question mark, a party already given, a pattern false positive). First-turn search rate unchanged (17 of 18 casual questions, 6 of 6 with dates). Frontmatter parses; `claude plugin validate .` passes; no internal paths, secrets or customer data added.

## Review round 2 and fixes — 2026-10-15 (still a draft: not pushed, not published)

The second review round confirmed most round-1 fixes and corrected one statement above. **Correction:** "the 8 it failed were checked by hand and meet the contract" was too strong. Two of those answers (both trip-planning prompts with this skill loaded) opened with itinerary or capability text before the sample sentence, and one also asked whether the traveller would rather stay outside the city searched; strictly, 22 of 24 opened with the sample sentence. The other explanations (several question marks in one line, a request without a question mark, a party already given, a pattern false positive) stand. No third-turn answer made any tool call.

Skill change: the sample sentence comes before any itinerary or other explanation; the one line asks only for what is missing; destination preferences also wait for the first own-date quotes; when the "Sample dates:" line says no prices came back, the answer starts with that fact and its reason. The matching server draft also stopped calling a refused or empty sample search "example prices" and now shows the hotel system's own error.

Re-test with a stricter grader (first sentence must be the sample sentence; asks counted per line; destination questions count as extra; the third turn is part of a full pass): 23 of 24 answers opened with the sample sentence, none asked whether to book, and none fetched rates or created a payment page on the sample dates in the third turn. Full contract: 11 of 12 with this skill loaded, 10 of 12 with the server instructions only. Of the three misses, one comes from the test data (the hotel asked about was not in the fixture, so the answer correctly began by saying so); two are minor ordering slips (the dates question placed after the closing statement, once with an extra "tell me if you'd like something cheaper"). First-turn search rate: 18 of 18 casual questions, 6 of 6 with dates. Frontmatter parses; `claude plugin validate .` passes.

## Review round 3 — 2026-10-15 (still a draft: not pushed, not published)

**Correction to round 2:** the round-2 figures are passes of an automated check, not proof of full compliance. With the destination check widened (it missed "Is Tokyo the only city, or do you also want hotels elsewhere …"), the round-2 re-test scores 10 of 12 with this skill loaded and 10 of 12 with the server instructions only; the check does not test where the booking note sits. Known deviations, none touching booking or prices: the dates question placed after the closing statement (twice, server only, once with an extra "tell me if you'd like something cheaper"); one trip-planning answer asking whether to look beyond the city searched; one answer placing a "this hotel did not come up" explanation before the booking note; and one answer opening with that explanation before the sample sentence (the test data lacked the hotel asked about, which explains it but is still an ordering slip; round 2 called it correct). All 24 third-turn answers made no tool call, and none asked whether to book.

No further wording change was made in this round: the remaining deviations are about order or one extra question, and the previous wording change shifted other answers. The offline checks run again at release, after both branches are rebased.

## Review round 4 — 2026-10-15

A narrow follow-up review of the round-3 changes returned "ready" with no findings; the record's re-test figures and listed deviations match the raw outputs. Still a local draft, held until the OpenAI app review passes; released together with the server branch, server first.

## Publication receipt — 2026-10-15 03:2x UTC (2026-10-14 PDT)

- **Approval.** The owner approved shipping on 2026-10-15, before the ChatGPT app review finished. This replaces the hold recorded above. The changed public search definition and server instructions become a held update in that review.
- **Merged and pushed.** `draft/public-search-first-2026-10-14` (4e83a5b, four review rounds with 10, 6, 3 and 0 findings) was merged into main with `--no-ff` as `e625609` and pushed to GitHub main; the remote ref matches. Version 1.1.10 in both manifests.
- **Matching service release.** The booking service release with the same behaviour went live at 03:10 UTC: on public connections the hotel search takes dates as optional and searches a labelled sample stay, and the server instructions ask one line for dates and party. Its tests include the cross-repository contract test against this 1.1.10 skill, which passed.
- **Directory status.** Pushing to GitHub does not by itself prove that the Claude directory serves 1.1.10. The owner confirms it on the plugin's directory management page and publishes the new version there if it is waiting. Installed copies then update on the directory side. Claude Code users who added the GitHub marketplace update as described in the README.
