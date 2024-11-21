# Simulating Scheduled Tasks with Prelude Operator

Scheduled tasks are a common technique attackers use to maintain persistence in a compromised system. This document demonstrates how to simulate and validate detection for scheduled task creation using Prelude Operator.

## MITRE ATT&CK Technique
- **T1053.005**: Scheduled Task/Job - Windows Task Scheduler

## Why Simulate Scheduled Tasks?
Simulating scheduled tasks helps test your Blue Team's ability to:
1. Detect task creation events.
2. Investigate suspicious use of task scheduling for persistence.
3. Improve correlation rules in SIEM tools like Elastic or Splunk.

## Prelude Operator Command Example
The following command simulates the creation of a scheduled task:
```bash
operator-cli run-technique --technique T1053.005
