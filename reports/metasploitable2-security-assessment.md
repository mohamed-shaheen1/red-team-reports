# Metasploitable 2 Security Assessment

## Executive summary

An internal penetration test of the intentionally vulnerable Metasploitable 2 VM identified multiple paths to unauthorized access and remote code execution. The dominant risks were default or weak credentials, exposed legacy services, missing brute-force controls, and outdated software.

## Scope and methodology

Testing followed a controlled workflow: planning, host and service discovery, vulnerability validation, limited exploitation, and reporting. Nmap, manual enumeration, and the Metasploit Framework were used only inside the isolated lab.

## Findings

| ID | Finding | Severity | Impact |
| --- | --- | --- | --- |
| RT-001 | Weak, default, and anonymous credentials | Critical | Unauthorized access to network services |
| RT-002 | Exposed Tomcat Manager with weak credentials | Critical | Deployment of attacker-controlled web content and RCE |
| RT-003 | Vulnerable Samba user-map script | Critical | Remote command execution |
| RT-004 | DVWA authentication lacked rate limiting | High | Automated password guessing |
| RT-005 | Legacy `r` services were exposed | Critical | Remote shell access and credential exposure |

## Key evidence

- FTP, SSH, Telnet, Tomcat, Samba, and vulnerable web applications were reachable.
- Default or weak credentials enabled access to administrative functionality.
- The Tomcat Manager accepted a deployable archive, demonstrating impact.
- The Samba configuration exposed a known command-execution path.
- Authentication endpoints allowed repeated attempts without lockout or throttling.

## Recommendations

1. Remove or firewall unnecessary services and replace legacy remote-shell protocols with SSH.
2. Eliminate default and shared credentials; enforce unique passwords and MFA for administration.
3. Upgrade Tomcat, Samba, the operating system, and all exposed applications.
4. Restrict management interfaces to trusted networks or VPN access.
5. Add rate limiting, account lockout, centralized logging, and alerts for password attacks.
6. Run recurring vulnerability assessments and verify remediation with retesting.

