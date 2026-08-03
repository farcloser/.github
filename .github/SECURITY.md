# Security

## Reporting a vulnerability

**Do not open a public issue for a security vulnerability.**

Every Farcloser repository has GitHub private vulnerability reporting enabled. Use it:

1. Go to the **Security** tab of the affected repository.
2. **Report a vulnerability** — or go straight to
   `https://github.com/farcloser/<repository>/security/advisories/new`.

That opens a private advisory visible only to you and the maintainers. It is the only
supported channel: it keeps the report confidential until a fix exists, and it is where
the advisory — and a CVE, if one is warranted — is published from.

If the repository has no Security tab (it should — that would be an error on our side),
report it privately against
[`farcloser/limen`](https://github.com/farcloser/limen/security/advisories/new) instead
and say which repository you meant.

## What to expect

An acknowledgement, and a fix on a **best-effort** basis.

There is no service-level agreement and no warranty of a timely patch — these projects are
provided as-is, see [SUPPORT.md](./SUPPORT.md). We will credit you in the advisory unless
you ask us not to.

## Scope

Reports are in scope when they concern code in this organization's repositories.

Out of scope: findings against third-party dependencies — report those upstream, though we
do want to hear about it if we are shipping a vulnerable pin — and reports that consist
only of an automated scanner's output with no demonstrated impact.
