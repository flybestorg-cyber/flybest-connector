# Maintaining this repository

Read [AGENTS.md](AGENTS.md) before starting and follow the [maintenance index](docs/maintenance/README.md).

Every change must include its reason and verification in a dated maintenance record, linked from the change log. The record should let the next maintainer understand what failed, why the chosen fix works, and which protection must stay. Reviewers check the linked prior records, changed behavior, evidence and actual release status alongside the code. Do not substitute a passing test count for examining the customer continuation path.

Use [the template](docs/maintenance/TEMPLATE.md). Keep historical reports unchanged; add a correction or follow-up entry when facts change. Keep customer and payment data out of examples. Documentation-only changes do not require a service restart. This is a repository maintenance policy, not a claim that branch protection automatically enforces reading or log updates.
