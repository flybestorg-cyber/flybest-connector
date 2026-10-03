# flybest-connector maintenance instructions

These instructions apply to every human and coding agent changing this repository.

## Before changing code
1. Read [the maintenance index](docs/maintenance/README.md) and [change log](docs/maintenance/CHANGELOG.md).
2. Find and read the records related to the affected flow, plus any linked tests and code comments. In the change record or PR, name the records consulted; if none applies, say so.
3. Check the current implementation and deployed-version evidence. A historical report is evidence about its recorded version, not proof of today's behavior. Do not restore a bug merely to match outdated prose.

## With every change
1. Add a dated record under `docs/maintenance/entries/` using [TEMPLATE.md](docs/maintenance/TEMPLATE.md), and append its link to `CHANGELOG.md` in the same commit or PR. This includes fixes, refactors, configuration, tool contracts and documentation behavior changes. Typo-only edits may use a short log entry with the reason and verification.
2. Explain the problem, root cause, precise fix, relevant alternatives or protections, customer-visible behavior, verification and remaining limits. Put short comments beside non-obvious logic explaining WHY, and link the record.
3. Keep the completion path usable: verified prices and terms can be accepted and continued; changed liabilities require fresh consent; explicit refusals and unknown provider outcomes are different. Do not remove money, identity or duplicate-write protections just to pass a test.
4. Separate local, committed, pushed and actually deployed status. Record the live release and health evidence after deployment; append later corrections and link the superseded statement instead of rewriting historical facts.
5. When another repository is affected, update its local record and link the related change. Keep this repository's scope intact.

## Repository boundary
This is a PUBLIC repository. Record only sanitized product behavior and public contracts. Do not copy private audit reports, infrastructure paths, credentials, customer data, live booking keys or internal security details here. Follow SECURITY.md for vulnerability reporting.

See [CONTRIBUTING.md](CONTRIBUTING.md). These instructions document the owner's maintenance requirement; they do not replace existing authorization or release procedures.
