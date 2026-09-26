# Hack The Box: Conceal

## Executive summary

Conceal was a Windows lab whose TCP services initially appeared filtered. UDP enumeration revealed IKE/ISAKMP and SNMP. SNMP data exposed the information needed to establish the IPsec connection, after which the underlying FTP, HTTP, RPC, NetBIOS, and SMB services became reachable. Anonymous FTP access and a web-accessible upload path created the documented route toward code execution.

## Attack path

1. Initial SYN scanning returned little useful information because TCP traffic was filtered.
2. UDP enumeration identified IKE on port 500 and an exposed SNMP service.
3. IKE negotiation confirmed the VPN attack surface, although aggressive mode did not directly yield useful key material.
4. SNMP enumeration disclosed the IPsec pre-shared key, which was weak enough to recover offline in the lab.
5. An IPsec tunnel was configured using the recovered settings.
6. TCP connect scanning through the tunnel exposed FTP, HTTP, RPC, NetBIOS, and SMB.
7. Anonymous FTP login succeeded. The otherwise empty FTP location was linked to a web upload directory.
8. The notes identify file upload as the intended access path but do not record a completed shell or privilege escalation.

## Key findings

- Perimeter filtering concealed services but did not remove the underlying exposure.
- SNMP disclosed sensitive VPN configuration data.
- A weak IPsec pre-shared key enabled unauthorized tunnel establishment.
- Anonymous FTP upload was connected to web-served content, creating a dangerous trust boundary.
- Multiple legacy Windows services increased the post-VPN attack surface.

## Risk

Disclosure of VPN secrets allows an attacker to cross the filtering boundary and enumerate internal services. An anonymous upload location mapped into a web directory may then permit malicious content placement and server-side code execution.

## Remediation

- Replace SNMPv1/v2c with SNMPv3 and restrict management access to dedicated hosts.
- Remove secrets from SNMP-accessible configuration and rotate the exposed IPsec key.
- Prefer IKEv2 with certificate authentication; use high-entropy PSKs only when necessary.
- Disable anonymous FTP and prevent upload directories from executing server-side content.
- Separate file-transfer storage from web roots and validate uploaded file types and names.
- Restrict RPC, NetBIOS, and SMB to required management segments and enable modern protections.

## Status

Incomplete. The source note establishes VPN access and the likely upload route, but it does not document a verified shell or administrator-level compromise.
