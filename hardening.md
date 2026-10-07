#Server Hardening 

Securing Linux server at a commercial level to prove I have the skills needed in a real world situation aswell as to secure my self, These test will be run through Wazuh, Lynus (add more here later)

## Baseline (2026-10-06)
| Metric | Before | After |

| Wazuh SCA (CIS Ubuntu) | 45% |
| Lynis hardening index| 60 |
| Lynis warnings/ sugestions | 2/55 |

## P1.01 SSH: keys only, no password login, no root login
**Why:** Preventing unauthorized user from getting into the system via unauthorized devices.
**Changes:** | Created an SSH Private key stored in Authorized Device| Changed SSH configuration on the Server to refuse Password logins|
**Verification:** - Config: [00-hardening.conf](../configs/ssh/00-hardening.conf)
