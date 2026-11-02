# 2026-11-02 Skill/README 1.1.13: say how to connect FlyBest when the tools are missing

- Record ID: 2026-11-02-plugin-connector-signin-1-1-13
- Date and time zone: 2026-11-02, America/Los_Angeles
- Related records: [2026-10-08-public-hotel-skill-refresh](2026-10-08-public-hotel-skill-refresh.md) (README explains the bundled Skill, the remote MCP connection and the separate e-mail sign-in), [2026-10-13-plugin-install-link](2026-10-13-plugin-install-link.md) (public plugin page), [2026-10-27-live-terms-wording-1-1-12](2026-10-27-live-terms-wording-1-1-12.md) (previous version).
- Affected files: `skills/flybest-hotels/SKILL.md` (section 9), `README.md` (Connect → Claude, Install in Claude Code), `.claude-plugin/plugin.json` and `lhm.plugin.json` (1.1.12 → 1.1.13).

## Problem and cause

A traveller ran `/flybest-hotels` in Claude for a hotel stay. Claude showed the plugin's Skill as loaded but answered that the hotel search and booking tools "didn't load into this chat", and suggested starting a new chat or checking settings. No rates were returned.

Most likely cause (consistent with the service's request logs, 2026-10-20 to 2026-11-02, and the plugin page; the individual traveller's account state was not inspected):

- The plugin bundles the remote MCP connection, which needs a one-time OAuth sign-in (e-mail code). On the plugin page the connector is listed under **Contents → Connectors**; on an account that already has a connector for the same URL it is shown as Connected.
- Since the plugin syncs to Claude Code surfaces (desktop agent, Cowork, VS Code, CLI and remote sessions), many such clients sent unauthenticated requests, received 401 (authentication required, the expected answer before sign-in), read the OAuth metadata and went no further: they never opened the sign-in page, so no e-mail address was entered and no code was sent. A handful completed client registration (6 registrations by the Claude Code plugin client in total). In the same period the e-mail sign-in itself worked: 163 public e-mail sign-ups in total, 47 in the last 14 days, mostly through Claude web chat, and signed-in users used the tools normally.
- Section 9 of the Skill covered an expired or missing sign-in only as "complete Claude's sign-in prompt". It said nothing for the case where the tools are absent from the chat altogether, so Claude improvised advice ("start a new chat") that cannot help an unsigned connection.
- The README told Claude users to "follow the prompts" and sign in "when prompted", but did not say how to start the sign-in when no prompt appears.

## Change and reason

- Skill section 9: a new first bullet for "the FlyBest tools are not in this chat at all". It names the usual cause (not signed in) and the other one (switched off for the chat), says a new chat alone does not fix an unsigned connection, and walks the traveller through checks in order: Customize → Connectors, Connect and the e-mail code if FlyBest is not connected; the + → Connectors toggle if it is; `/mcp` for `plugin:flybest-hotels:flybest` in Claude Code; then a new chat. If FlyBest is connected and switched on and the tools are still missing, the cause is left open and the advisor contact is offered. Web search is offered only as a stopgap because it has no bookable rates or partner benefits. The existing "authentication expired" bullet is kept for tool calls that return an authorization error.
- README Connect → Claude: connecting the plugin's FlyBest connector (Customize → Connectors → Connect) is now an explicit step, and the README says what the traveller sees until it is done.
- README Install in Claude Code: says that while `claude mcp list` or `/mcp` shows the server as needing authentication (also when the plugin arrived through account sync), the tools stay unavailable until the `/mcp` sign-in is done.
- Version 1.1.13 so installed plugins pick up the Skill change.

No tool, server instruction or booking behaviour changes. Money, consent and booking protections are untouched.

## Customer experience and compatibility

A traveller whose FlyBest connection was never signed in now gets the exact place to click and the e-mail-code step, instead of being told to retry. Travellers who are already connected see no difference. Installed plugins need 1.1.13 to receive the new Skill text; the ChatGPT package is built separately and is not changed by this record.

## Verification

- Plugin page (authenticated, 2026-11-02): version 1.1.12 serving; Contents lists Skills 1 and Connectors 1 (flybest); on an account with an existing connector for the same URL the connector shows as Connected.
- Request-log review as summarised above (counts and client families only; no customer data recorded here).
- `claude plugin validate` on the changed plugin and marketplace, and the service repository's contract test that pins the plugin version (updated to 1.1.13 there): results in the release receipt below.

## Version and release status

- Commit: see this record's Git commit.
- GitHub push: pending at the time of writing; receipt to be appended.
- Claude directory: confirm 1.1.13 is serving after the push; publish manually from the management page only if the automatic pickup does not; receipt to be appended.
- No service restart or backend deployment.
- Release receipt (checked 2026-11-02, 15:05 PST): `1f3ec21` (1.1.13) was pushed to `origin/main`, but the Claude directory never listed it as a version: the next push (`3643b55`, 1.1.14) arrived before pickup and only that commit was scanned. 1.1.14 carries every 1.1.13 change and has been live since 13:48 PST; see [2026-11-02-signin-reminder-1-1-14](2026-11-02-signin-reminder-1-1-14.md). No manual publish was needed.

## Remaining limits

The connector still requires a sign-in before any tool appears; Claude's own clients decide whether to prompt for it. Whether search should work without a sign-in is a product decision for the owner and is not changed here. Customize → Connectors and + → Connectors are from Claude's connector documentation; the plugin page's Contents → Connectors listing was observed on 2026-11-02. Labels may change with Claude releases. Whether a given Claude Code surface ever starts the sign-in on its own was not measured; the logs only show that most did not reach it.
