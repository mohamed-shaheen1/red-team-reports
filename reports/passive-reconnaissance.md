# Passive Reconnaissance Methodology

## Objective

Collect publicly available information about an organization without sending intrusive traffic or attempting access.

## Sources

- DNS and certificate-transparency records.
- Search engines and the organization's public website.
- Public email-pattern and employee information.
- Passive subdomain datasets and historical DNS.
- Public technology and hosting metadata.

## Workflow

1. Confirm written scope, permitted sources, and data-retention rules.
2. Resolve public domains and record authoritative DNS data.
3. Enumerate subdomains from passive sources and deduplicate results.
4. Identify likely email-address patterns without contacting or testing accounts.
5. Classify assets by business function and exposure.
6. Timestamp each observation and retain the source URL.

## Reporting cautions

Passive datasets may be stale, incorrect, or contain third-party infrastructure. A discovered hostname is not proof of ownership or vulnerability. Do not publish employee addresses, internal-looking hostnames, or sensitive infrastructure details without authorization.

## Deliverable

Provide an asset inventory with source, first/last observed dates, confidence, and recommended validation. Summarize counts and exposure themes rather than publishing a raw sensitive list.

