# 2026-11-03 Restore privacyPolicyUrl in the Claude manifest

- Record ID: 2026-11-03-privacy-policy-url
- Date and time zone: 2026-11-03, Los Angeles (PST)
- Related records: [2026-10-07-hotel-skills-conversion](2026-10-07-hotel-skills-conversion.md) (removed the key in 1.1.6), [2026-10-08-public-hotel-skill-refresh](2026-10-08-public-hotel-skill-refresh.md) (kept it out as a known note), [2026-11-02-signin-reminder-1-1-14](2026-11-02-signin-reminder-1-1-14.md) (latest release receipt).
- Affected files: `.claude-plugin/plugin.json`, `README.md`. No Skill, tool or server change.

## Problem and root cause

Every Claude directory version since 1.1.6 shows the validation note "No privacy policy URL" (`.claude-plugin/plugin.json · privacyPolicyUrl`). The key was removed on 2026-10-07 because Claude Code 2.1.72 rejected it as unknown. The listing itself already names the privacy notice (captured at submission), but the manifest did not.

## Change

`privacyPolicyUrl` is restored as `https://ai.flybest.org/privacy`, the same address as the listing and the README's "Terms, privacy, security" section. `displayName` stays out. The version stays 1.1.14: no customer-visible behaviour changes.

## Compatibility and verification (2026-11-03)

- `claude plugin validate .` with the key: Claude Code 2.1.316 (current) passes with nothing to report; 2.1.250 passes and notes the field as unknown and ignored at load; 2.1.150 and 2.1.76 pass.
- Real install from a local marketplace copy (`plugin marketplace add` + `plugin install flybest-hotels@flybest`, isolated HOME): succeeds on 2.1.76 and 2.1.316, and the installed manifest carries the key.
- 2.1.76 is the oldest version that installs this plugin at all (bisected 2026-11-02), so restoring the key loses no client.
- `https://ai.flybest.org/privacy` answers HTTP 200.

## Version and release status

- Commit: see this record's Git commit. Push to `main` and the directory receipt to be appended.

## Remaining notes

The other standing directory notes are unchanged and deliberate:
- `icon.png` passed without a code check: it is a plain PNG.
- The listing icon cannot be changed from the manifest. Claude takes a manifest icon only at first submission, and this listing recorded it as a path the portal does not display. It shows a letter until an image is uploaded in the developer portal's Listing tab, which is the owner's action.
- The credential warning concerns the connector's sign-in, which the user starts; the plugin reads nothing from the user's machine.
- A Markdown record is flagged as an image or font that code could run. It is plain text and nothing runs it.
- The root `CLAUDE.md` is maintainer context, not plugin context.
