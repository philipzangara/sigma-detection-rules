# sigma-detection-rules

Sigma detection rules for common adversary TTPs mapped to MITRE ATT&CK, with converted Splunk SPL queries and sanitized sample logs for testing.

## Rules

| Rule | MITRE Technique | Log Source | Level |
|------|----------------|------------|-------|
| T1059.001 - Suspicious PowerShell Execution | Execution | Sysmon (EventCode 1) | Medium |
| T1110 - Failed Logon Attempts (Brute Force) | Credential Access | Security (EventCode 4625) | Medium |
| T1078 - Suspicious Logon | Initial Access | Security (EventCode 4624) | Medium |

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

Convert to Splunk SPL:
```
sigma convert -t splunk -p splunk_windows -p splunk_sysmon_acceleration rules/execution/T1059_001_powershell_execution.yml
sigma convert -t splunk -p splunk_windows rules/credential_access/T1110_brute_force_logon.
sigma convert -t splunk -p splunk_windows rules/initial_access/T1078_suspicious_logon.yml
```

## Sample Logs

Sanitized sample logs are included in `tests/sample_logs/` to validate each rule without requiring a live environment.

## Author: Philip Zangara

## License: MIT

Disclaimer: Built independently, with AI used as a learning aid for guidance and debugging feedback.