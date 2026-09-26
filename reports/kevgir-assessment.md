# Kevgir VM Assessment

## Summary

The Kevgir lab exposed several services. The most significant path used Tomcat Manager on TCP/8080 with weak credentials, allowing deployment of server-side content and command execution. Redis was also reachable and permitted unauthenticated inspection.

## Attack path

1. Host discovery identified `192.168.213.129` in the lab network.
2. Port and version scanning revealed a broad attack surface.
3. Web enumeration located Tomcat Manager on port 8080.
4. Weak credentials allowed access to the management interface.
5. Controlled deployment demonstrated command execution.
6. Redis accepted commands but contained no useful keys in the observed database.

## Risk

Exposed application-management interfaces combined with weak credentials can lead directly to remote code execution. An unauthenticated Redis service may disclose or modify application data and, depending on host permissions and configuration, enable further compromise.

## Remediation

- Restrict Tomcat Manager to an internal management network and enforce strong unique credentials.
- Disable deployment functionality when it is not required.
- Bind Redis to trusted interfaces, require authentication, and apply network ACLs.
- Patch both services and monitor administrative actions.

