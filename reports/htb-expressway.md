# Hack The Box: Expressway

## Executive summary

Expressway demonstrated why UDP enumeration matters when a conventional TCP scan appears sparse. SSH was the only obvious TCP service, while UDP discovery exposed IKE/ISAKMP. IKE enumeration yielded material that allowed recovery of the lab pre-shared key, leading to valid SSH access. The recorded privilege-escalation path then used a vulnerable sudo release to obtain root.

## Attack path

1. TCP enumeration identified SSH but little additional attack surface.
2. A UDP scan exposed IKE/ISAKMP, prompting focused VPN enumeration.
3. IKE negotiation confirmed that the target accepted a Phase 1 proposal.
4. Aggressive-mode exchange data exposed material suitable for offline pre-shared-key recovery.
5. The recovered lab credential was associated with a valid SSH user and provided an initial foothold.
6. Local enumeration did not reveal an obvious misconfiguration but identified sudo 1.9.17.
7. The lab host was vulnerable to CVE-2025-32463, providing a verified path to root.

## Key findings

- UDP services exposed a critical attack surface that TCP-only scanning would miss.
- IKE configuration allowed offline recovery of a weak pre-shared key.
- VPN-related credentials were reusable for SSH access.
- An unpatched privileged component enabled local privilege escalation.

## Risk

Weak IKE authentication can expose reusable credentials without generating a normal interactive login. Once a foothold is established, a vulnerable sudo installation can turn a low-privilege account into full host compromise.

## Remediation

- Prefer certificate-based IKEv2 authentication and disable IKEv1 aggressive mode.
- Use long, randomly generated pre-shared keys where PSKs cannot be eliminated.
- Never reuse VPN secrets for operating-system accounts.
- Restrict IKE exposure to expected peers and monitor unusual negotiations.
- Upgrade sudo to a vendor-fixed release and maintain an inventory of privileged packages.
- Include UDP services in vulnerability management and external attack-surface reviews.
