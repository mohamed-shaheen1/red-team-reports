# Kioptrix Enumeration Report

## Objective

Enumerate an intentionally vulnerable Kioptrix VM and identify services requiring deeper validation.

## Discovery

An all-ports Nmap scan identified:

| Port | Service | Observation |
| --- | --- | --- |
| 22/TCP | OpenSSH 2.9p2 | Legacy release and SSHv1 support |
| 80/TCP | Apache 1.3.20 | Old web server; TRACE enabled |
| 111/TCP | rpcbind | RPC services exposed |
| 139/TCP | Samba 2.2.x | High-priority legacy-service lead |
| 443/TCP | Apache/mod_ssl | Expired certificate and SSLv2 support |
| 32768/TCP | RPC status | Additional RPC exposure |

## Analysis

The attack surface is dominated by obsolete software. Samba versioning, SSLv2 support, SSHv1, and old Apache/mod_ssl components should be validated against the exact build and configuration before exploitation. Version banners alone can be misleading, so each potential vulnerability needs a safe confirmation step.

## Recommendations

- Upgrade or remove legacy SSH, Apache, OpenSSL, and Samba components.
- Disable SSHv1, SSLv2, TRACE, and unnecessary RPC services.
- Restrict administrative services to trusted management networks.
- Use authenticated scanning and configuration review to verify patch state.

