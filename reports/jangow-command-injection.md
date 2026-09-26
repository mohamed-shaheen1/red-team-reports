# Jangow Command-Injection Assessment

## Summary

The Jangow lab exposed FTP and HTTP. Anonymous FTP access was not available, but web content enumeration revealed a user-controlled parameter that executed operating-system commands.

## Attack path

1. Host discovery established the target address.
2. Service scanning identified FTP and HTTP.
3. Directory enumeration found a WordPress-related path and additional content.
4. A page parameter accepted system commands; harmless commands confirmed command injection.
5. File-system enumeration located a backup file containing credentials.
6. The recovered credentials enabled access to the lab host.

## Risk

Unauthenticated command injection provides an attacker with remote command execution in the web-service context. Credential material stored in a web-accessible or readable backup file turns that initial foothold into authenticated system access.

## Remediation

- Never pass user input to a shell. Use safe library calls and strict allowlists.
- Remove backup files from web roots and rotate every exposed credential.
- Run the web service with a low-privilege account and apply mandatory access controls.
- Log parameter anomalies and alert on command separators and unexpected child processes.

