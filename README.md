# AWS IP Lists

All IP ranges that Amazon Web Services publishes for its services and regions, as plain text
lists ready for firewalls, WAFs and log enrichment.

## Files

| File | Contents | Raw URL |
|---|---|---|
| `aws_ip_range.lst` | IPv4 prefixes | https://raw.githubusercontent.com/SecOps-Institute/AWSIPLists/master/aws_ip_range.lst |
| `aws_ipv6_range.lst` | IPv6 prefixes | https://raw.githubusercontent.com/SecOps-Institute/AWSIPLists/master/aws_ipv6_range.lst |
| `Last-Checked-At` | Time of the last successful check (IST) | |

Each file has one CIDR per line. Entries are normalized, deduplicated and sorted numerically,
with no comments.

## How it is built

- Source: Amazon's official feed, https://ip-ranges.amazonaws.com/ip-ranges.json
- Every `prefixes[].ip_prefix` goes into the IPv4 list, and every `ipv6_prefixes[].ipv6_prefix`
  into the IPv6 list.
- The feed lists the same prefix once per service. Duplicates are removed here.
- To filter by service or region (for example only `CLOUDFRONT` or only `eu-west-1`), use
  the upstream JSON directly.

## Update schedule

**mirabot**, an automated bot, checks the source **every hour**:
- `Last-Checked-At` is updated on every successful check.
- The list files change only when AWS actually adds or removes ranges, so this repo's commit
  history doubles as a change log.

Before publishing, the bot checks each update for problems: minimum size, malformed data, and
any sudden drop of more than half the entries. If a check fails, the previous list stays in
place. If `Last-Checked-At` is more than a few hours old, an update is being held back or the
bot is down.

## Notes

- These are AWS-owned ranges, but most of them host **AWS customers' workloads**. Being in this
  list means "runs on AWS", not "is Amazon".

## License

MIT for this repository. The data comes from Amazon's public `ip-ranges.json`.

---
Updated hourly by **mirabot**, sponsored by [endlesstokens.ai](https://endlesstokens.ai) — *Pay for Time not Tokens*.

Maintained by [SecOps Institute](https://github.com/SecOps-Institute) ·
[LinkedIn](https://www.linkedin.com/in/aarvee11) · [Blog](https://amisafe.secops.in)
