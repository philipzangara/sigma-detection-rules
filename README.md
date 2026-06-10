# sigma-detection-rules

Sigma detection rules for common adversary TTPs mapped to MITRE ATT&CK, with converted Splunk SPL queries and sanitized sample logs for testing.

## Rules

| Rule | MITRE Technique | Log Source | Level |
|------|----------------|------------|-------|
| T1059.001 - Suspicious PowerShell Execution | Execution | Sysmon (EventCode 1) | Medium |
| T1110 - Failed Logon Attempts (Brute Force) | Credential Access | Security (EventCode 4625) | Medium |
| T1078 - Suspicious Logon | Initial Access | Security (EventCode 4624) | Medium |
| T1003.001 - LSASS Credential Dump | Credential Access | Sysmon (EventCode 1) | Medium |
| T1562.001 - Security Log Clearing | Defense Evasion | Security (EventCode 1102) | Medium |

## Repository Structure

```
sigma-detection-rules/
├── rules/           # Sigma rules organized by MITRE tactic
├── tests/
│   └── sample_logs/ # Sanitized sample logs for each rule
├── splunk/          # Converted Splunk SPL queries
└── README.md
```

## Requirements

- [sigma-cli](https://github.com/SigmaHQ/sigma-cli)
- Splunk backend plugin: `sigma plugin install splunk`

## Converting Rules

Convert any rule to Splunk SPL using sigma-cli. Use `splunk_sysmon_acceleration` pipeline for Sysmon-based rules:

```
# Sysmon rules (EventCode 1, 10, etc.)
sigma convert -t splunk -p splunk_windows -p splunk_sysmon_acceleration rules/<tactic>/<rule>.yml

# Security log rules (EventCode 4624, 4625, 1102, etc.)
sigma convert -t splunk -p splunk_windows rules/<tactic>/<rule>.yml
```

Pre-converted SPL queries are available in the `splunk/` folder.


## Sample Logs

Sanitized sample logs are included in `tests/sample_logs/` to validate each rule without requiring a live environment.

## Author: Philip Zangara

## License: MIT

Disclaimer: Built independently, with AI used as a learning aid for guidance and debugging feedback.