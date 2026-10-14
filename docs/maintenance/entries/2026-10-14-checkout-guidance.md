# 2026-10-14 Checkout continuation and public guidance (1.1.9)

- Consulted: maintenance README/CHANGELOG, 2026-10-04 public contract, 2026-10-08 Skill refresh, 2026-10-11 wording and 2026-10-14 updating records.
- Scope: public hotel Skill, security contact and two plugin version manifests. Related backend maintenance: 2026-10-14-review-public-guidance (private repository; no private operational details copied here).

## Problem and change

The Skill did not distinguish link-creation failures from a page that already exists and offers revised terms. It now explains that RATE_CHANGED_BEFORE_BOOKING/RATE_UNAVAILABLE at creation produce no page: repeat the same search, compare the new row, obtain any required agreement, then request a link. Existing-page reconfirmation remains the preferred continuation when offered.

Payment-timing advisories must be read: disclose a possible charge at booking before sharing; withhold a link when the result says timing is unverified. Family quote expiry first triggers a search with the same actual occupancy and ages, never removal of children. The normal three-open-page limit and returned closure notices are explained; multiple separate rooms can proceed in completed batches or with advisor help. SECURITY.md uses jay@flybest.org. Both plugin manifests are prepared as version 1.1.9.

## Compatibility and verification

The same eight public hotel tools remain. Verified rates still lead to booking; changed liabilities need agreement, and submitted or unknown attempts are checked before replacement. No private saved-card, flight or advisor-only tools are introduced. The backend terms wording is aligned with same-page reconfirmation.

Static verification covers manifest versions, public tool names, relative links and required continuation guidance. No real booking, charge, cancellation or message was sent. These are instruction/packaging checks, not an end-to-end model behaviour claim. Both JSON manifests parse as 1.1.9; the Skill frontmatter, required continuation instructions, updated contact and maintenance links pass static checks. The patch passes git diff --check.

## Publication status

Base 4c96779b0276a620645cc40874e5bde7a13bd205. Changes are on fix/codex-review-repairs-20261014; see this record's Git commit. Not published or deployed while preparing this record. Publication must be recorded separately; setting a manifest version does not publish a plugin.

## Follow-up to earlier wording

The 2026-10-14 updating note's statement that the Skill needed no changes was about that earlier review. This later checkout review found the above guidance gaps; the old record is preserved as history.
