# Hack The Box: CodePartTwo

## Executive summary

CodePartTwo exposed a web application and a code-execution service on ports 80 and 8000. Reviewing the downloadable application source revealed `js2py` 0.74, whose Python-import restriction could be bypassed in this lab. The resulting command execution enabled host enumeration, recovery of a stored password hash from SQLite, and authenticated SSH access.

## Attack path

1. Service enumeration identified HTTP applications on ports 80 and 8000.
2. Application source was downloaded and reviewed to understand the server-side code-execution design.
3. Dependency review identified `js2py` 0.74 and an unsafe sandbox boundary associated with CVE-2024-28397.
4. A proof-of-concept confirmed operating-system command execution from the JavaScript execution context.
5. System enumeration confirmed a Linux host and revealed an accessible SQLite database.
6. A stored password hash was extracted and recovered offline in the authorized lab.
7. The recovered account material enabled SSH access as a local user.
8. SUID binaries and other privilege-escalation candidates were enumerated, but no verified root path was recorded.

## Key findings

- Untrusted code was processed by a dependency that did not provide a reliable security boundary.
- A vulnerable third-party package converted application functionality into remote command execution.
- Recoverable password material in SQLite enabled movement from the application context to SSH.
- Local privilege-escalation enumeration found several candidates, but the notes do not establish exploitability.

## Risk

Remote command execution compromises the confidentiality and integrity of application data and the host account running the service. Weak password storage and credential reuse can then turn a limited service foothold into interactive system access.

## Remediation

- Do not treat language runtimes or package-level restrictions as a hardened sandbox for hostile code.
- Isolate code execution in short-lived containers or VMs with no host secrets, no unnecessary network access, strict resource limits, and a read-only base image.
- Remove the affected `js2py` version and verify the security properties of any replacement.
- Store passwords with a modern adaptive password hash and unique salts; rotate exposed credentials.
- Prevent credential reuse between applications and operating-system accounts.
- Restrict SSH and monitor unusual child processes spawned by web services.

## Status

User-level access was documented. Root compromise was not verified in the source note and is not claimed here.
