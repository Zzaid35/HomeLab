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
**Verification:** - Config: [00-hardening.conf](/configs/ssh/00-hardening.conf)
**Findings:** With password authentication disabled, failed login attempts no longer appear as authentication failures. Attackers disconnect before authenticating, which Wazuh logs as level-4 "connection reset" events, and its built-in brute-force rule doesn't count those. I wrote a custom rule [Local_rules.xml](configs/wazuh) that raises a level-10 alert when one IP produces 5 of these disconnects within 60 seconds. [Wazuh rule 100101 firing](docs/image/100101.png)

