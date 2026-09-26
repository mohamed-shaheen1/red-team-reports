# Hack The Box: Planning

## Executive summary

Planning was an authorized Hack The Box lab focused on web enumeration, virtual-host discovery, exploitation of a vulnerable Grafana deployment, and post-exploitation credential discovery. Initial browsing and directory enumeration did not expose a useful path; virtual-host enumeration revealed the additional application surface that enabled progress.

## Attack path

1. A TCP scan identified SSH on port 22 and HTTP on port 80.
2. The target hostname was mapped locally so the name-based web service could be reached.
3. Directory and proxy-assisted testing produced no confirmed vulnerability on the primary site.
4. Virtual-host enumeration identified an additional Grafana service.
5. Credentials supplied for the lab enabled authentication to Grafana.
6. The deployed Grafana 11.0 instance was affected by a remote-code-execution path, which provided a shell in the lab environment.
7. Local enumeration exposed credentials for a system user, allowing SSH access and recovery of the user proof.

## Key findings

- The web attack surface depended on hostname-based routing and was not obvious from IP-only browsing.
- A vulnerable administrative application enabled remote command execution after authentication.
- Reusable credentials were exposed to a compromised application context.
- Host-level secrets turned application compromise into direct system access.

## Risk

An attacker with access to the Grafana account could execute commands in the application context. Credentials exposed on the host could then support lateral movement or a more stable SSH foothold.

## Remediation

- Upgrade Grafana to a release that addresses the applicable vulnerability and remove unused plugins or features.
- Restrict administrative interfaces to a management network and require strong, unique credentials with MFA where supported.
- Keep service credentials out of environment variables, command lines, and broadly readable files.
- Run monitoring and analytics services with minimal operating-system privileges.
- Inventory virtual hosts and ensure each one receives the same security testing and patch management as the primary site.

## Status

The source notes document access through the user-level foothold. A root-level privilege-escalation path was not recorded, so this report does not claim full system compromise.
