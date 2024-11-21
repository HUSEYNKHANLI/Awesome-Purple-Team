# Bash Examples for Atomic Red Team

## Simulating Linux Commands
Test malicious file execution:
```bash
./atomic-test.sh -t T1059.004 -f "/tmp/test.sh"
