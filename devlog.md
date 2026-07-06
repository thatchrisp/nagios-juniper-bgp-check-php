# nagios-juniper-bgp-check-php — Dev Log

## Summary

`nagios-juniper-bgp-check-php` is a single-file Nagios/Icinga plugin, `check_bgp`, written in PHP, that monitors the state of a BGP neighbor on a Juniper device over SNMP v2c. It takes positional arguments (`host`, `community`, `remote_peer`, `local_peer`) and polls the standard BGP4-MIB peer-state OID (`1.3.6.1.2.1.15.3.1.2.<remote_peer>`) via `snmp2_get()`.

Peer states 1–5 (idle/connect/active/opensent/openconfirm) return `CRITICAL` (exit 2). When the peer is `established` (state 6) the script drills into Juniper's enterprise MIB (`jnxBgpM2`, OID base `1.3.6.1.4.1.2636.5.1.1.2`) to resolve the peer index and read the received-route count, returning `OK` (exit 0) with a human-readable route count. Any unexpected state returns `UNKNOWN` (exit 3). The `README.md` documents the matching Nagios `command` definition.

This is a tiny, dependency-light utility repo (no framework, no build). The `#!/path/to/php` shebang is a placeholder the operator edits to point at their local PHP binary. Git history is short: initial commit, a README code-block fix, a PHP-path update in the script, and the `.gitattributes` LF-enforcement commit.

---

## Todo

- The `#!/path/to/php` shebang is a placeholder and must be edited to the deployment host's PHP interpreter path before use.
- Requires the PHP SNMP extension (`snmp2_get`) to be installed on the monitoring host.

---

## Progress

### 2026-07-06 — devlog added

Added `devlog.md` per the portfolio devlog standard. The repo is a stable single-file PHP Nagios plugin for checking Juniper BGP neighbor state (and established-session route counts) over SNMP; the most recent change was a `.gitattributes` LF-enforcement commit.
