# Windows 7 SMB / MS17-010 Assessment

## Summary

Enumeration of an intentionally vulnerable Windows 7 VM identified SMB exposure consistent with MS17-010. A non-destructive scanner module confirmed vulnerability before exploitation was attempted in the lab.

## Validation process

1. Confirm host ownership and lab scope.
2. Enumerate SMB ports, dialects, signing, and operating-system indicators.
3. Use a vulnerability-check module before any exploit module.
4. Record target and listener configuration.
5. Demonstrate impact once, then stop and preserve evidence.

The automated path created a session successfully. A separate manual exploit attempt initially crashed the VM, demonstrating the operational risk of kernel exploitation even in a controlled environment.

## Risk

Successful exploitation may provide system-level execution and can also cause denial of service. On production networks, the same exposure supports wormable lateral movement.

## Remediation

- Apply Microsoft security updates for MS17-010.
- Disable SMBv1 and restrict TCP/445 between network segments.
- Monitor for SMB exploit signatures, unusual named-pipe activity, and lateral movement.
- Replace unsupported Windows versions.

