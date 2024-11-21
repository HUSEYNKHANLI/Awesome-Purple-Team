# Persistence Techniques Examples with Prelude Operator

Persistence techniques allow attackers to maintain access to a compromised system even after reboots or credential changes. This document demonstrates how to simulate and validate multiple persistence mechanisms using Prelude Operator.


## Example 1: Scheduled Tasks (T1053.005)
Attackers often use scheduled tasks to execute malicious payloads at specific intervals.

### Command to Simulate Scheduled Task Creation
```bash
operator-cli run-technique --technique T1053.005

## Example 2: DLL Hijacking (T1574.001)
Attackers place malicious DLLs in directories prioritized by the operating system's search order to hijack legitimate processes.

### Command to Simulate DLL Hijacking
```bash
operator-cli run-technique --technique T1574.001
