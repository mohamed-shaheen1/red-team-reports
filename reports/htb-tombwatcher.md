# Hack The Box: TombWatcher

## Executive summary

TombWatcher was approached as an Active Directory enumeration lab. Network and SMB enumeration identified the `tombwatcher.local` domain, but the documented attempt stopped after an RPC authentication failure. This report preserves the useful discovery work without presenting the machine as completed.

## Assessment activity

1. Network scanning was used to identify the exposed services and indicators of an Active Directory environment.
2. SMB and NetBIOS enumeration identified the domain name `tombwatcher.local`.
3. An authenticated RPC enumeration attempt returned `NT_STATUS_LOGON_FAILURE`.
4. The failure was treated as an authentication problem rather than evidence that RPC was unavailable.

## Key findings

- The target exposed enough Windows-domain metadata to identify its Active Directory namespace.
- The tested credential set was not accepted by the RPC service.
- No verified foothold, privilege escalation, or proof-file recovery was recorded in the source notes.

## Recommended next steps

- Reconfirm the lab-provided credentials, domain format, username format, and time synchronization.
- Enumerate Kerberos, LDAP, SMB signing, shares, and account-policy information using non-destructive checks.
- Build a domain map from evidence before attempting credential attacks.
- Record tool output and distinguish anonymous, guest, and authenticated results.

## Defensive takeaways

- Limit anonymous SMB and RPC information disclosure.
- Require SMB signing where operationally possible and disable obsolete protocols.
- Monitor repeated authentication failures and unusual enumeration across domain services.
- Avoid descriptive domain and host metadata where it is not operationally necessary.

## Status

Incomplete. The source note records domain discovery and an authentication failure only; no compromise is claimed.
