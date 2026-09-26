# Linux Privilege-Escalation Assessment

## Summary

The lab exposed a web shell through a `shell.php` endpoint. After gaining a low-privilege shell, enumeration identified two possible escalation classes: a kernel-level issue and an unsafe SUID binary.

## Workflow

1. Discover the host and enumerate all listening services.
2. Identify the command-execution endpoint and confirm it with harmless commands.
3. Establish a controlled shell in the isolated lab.
4. Record kernel, distribution, architecture, users, groups, mounts, capabilities, and SUID files.
5. Validate exploit suggestions against the exact kernel and configuration.
6. Prefer the least disruptive path and document the resulting privilege level.

## Findings

- Web command execution provided the initial foothold.
- The installed kernel matched a known escalation candidate.
- A misconfigured SUID executable ultimately provided root access.

## Remediation

- Remove the web shell and fix the application flaw that allowed its placement or execution.
- Patch the kernel and unsupported packages.
- Audit SUID/SGID files and remove elevated bits that are not operationally required.
- Mount writable data partitions with `nosuid` where appropriate.
- Alert on privilege transitions and execution from temporary directories.

