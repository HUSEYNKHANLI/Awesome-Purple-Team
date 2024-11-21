# Persistence Techniques Examples with Prelude Operator

Persistence techniques allow attackers to maintain access to a compromised system even after reboots or credential changes. This document demonstrates how to simulate persistence mechanisms using Prelude Operator to test and validate detection capabilities.

## Table of Contents
- [Example 1: Scheduled Tasks](#example-1-scheduled-tasks-t1053005)
- [Example 2: Registry Run Keys/Startup Folder](#example-2-registry-run-keysstartup-folder-t1547001)
- [Example 3: Create New Service](#example-3-create-new-service-t1543003)
- [Example 4: DLL Search Order Hijacking](#example-4-dll-search-order-hijacking-t1574001)
- [Example 5: Boot or Logon Initialization Scripts](#example-5-boot-or-logon-initialization-scripts-t1037001)
- [Example 6: Office Application Startup](#example-6-office-application-startup-t1137001)
- [Example 7: Modify System Boot Configuration](#example-7-modify-system-boot-configuration-t1542001)
- [Example 8: Application Shimming](#example-8-application-shimming-t1546011)
- [Example 9: Netsh Helper DLL](#example-9-netsh-helper-dll-t1546007)

## Example 1: Scheduled Tasks (T1053.005)

Attackers often use scheduled tasks to execute malicious payloads at specific intervals.

### Command to Simulate Scheduled Task Creation
```bash
operator-cli run-technique --technique T1053.005
```

### Example Behavior
- A scheduled task named ExampleTask is created to run cmd.exe at a specific time
- This command simulates creating a malicious scheduled task to maintain persistence

### Detection Suggestions
- Monitor for commands invoking schtasks.exe or Task Scheduler
- Alert on unusual task names or tasks created by non-administrative users

## Example 2: Registry Run Keys/Startup Folder (T1547.001)

Adding malicious scripts or executables to startup locations ensures they are executed when the system reboots.

### Command to Simulate Registry Persistence
```bash
operator-cli run-technique --technique T1547.001
```

### Example Behavior
- A registry key is added to the `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` path
- The registry key points to a malicious executable located in `%TEMP%\malware.exe`

### Detection Suggestions
- Monitor changes to the registry path `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`
- Alert on suspicious binaries or scripts being added to startup locations

## Example 3: Create New Service (T1543.003)

Attackers may create new services to execute malicious binaries under the guise of legitimate processes.

### Command to Simulate Service Creation
```bash
operator-cli run-technique --technique T1543.003
```

### Example Behavior
- A new service named MaliciousService is created to execute a binary like `C:\temp\malware.exe`
- Services created outside standard directories should trigger detection

### Detection Suggestions
- Monitor service creation events in system logs
- Correlate service binary paths with known legitimate directories

## Example 4: DLL Search Order Hijacking (T1574.001)

Attackers can replace or plant malicious DLLs to hijack legitimate processes.

### Command to Simulate DLL Hijacking
```bash
operator-cli run-technique --technique T1574.001
```

### Example Behavior
- A malicious DLL named example.dll is placed in a directory higher in the search order
- When a legitimate application runs, it loads the attacker-controlled DLL instead of the original

### Detection Suggestions
- Monitor directories where critical applications load DLLs
- Alert on unusual or modified DLL files in application paths

## Example 5: Boot or Logon Initialization Scripts (T1037.001)

Initialization scripts can execute commands or malware during boot or user login.

### Command to Simulate Logon Script Persistence
```bash
operator-cli run-technique --technique T1037.001
```

### Example Behavior
- A script is added to the startup folder to execute during user logon
- The script runs a malicious payload located in `C:\Users\Public\startup_script.bat`

### Detection Suggestions
- Monitor changes to `C:\Users\[User]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`
- Alert on unauthorized script files in the startup folder

## Example 6: Office Application Startup (T1137.001)

Malicious add-ins for Microsoft Office applications can execute attacker-controlled code.

### Command to Simulate Malicious Office Add-In
```bash
operator-cli run-technique --technique T1137.001
```

### Example Behavior
- An attacker places a malicious add-in.dll in the Office add-ins directory
- Office applications like Word or Excel execute the malicious code when launched

### Detection Suggestions
- Monitor directories like `%APPDATA%\Microsoft\Word\STARTUP` or `%APPDATA%\Microsoft\Excel\XLSTART`
- Alert on unexpected DLLs in these directories

## Example 7: Modify System Boot Configuration (T1542.001)

Attackers modify system boot configuration to execute malicious code during the boot process.

### Command to Simulate Boot Configuration Modification
```bash
operator-cli run-technique --technique T1542.001
```

### Example Behavior
- The boot configuration data (BCD) is altered to include a malicious driver or application
- This ensures execution of the payload early in the boot process

### Detection Suggestions
- Monitor changes to the boot configuration using commands like bcdedit
- Alert on unauthorized modifications to boot-critical files or settings

## Example 8: Application Shimming (T1546.011)

Attackers create custom shims to intercept and modify application behavior for persistence.

### Command to Simulate Application Shimming
```bash
operator-cli run-technique --technique T1546.011
```

### Example Behavior
- A custom shim is created for a legitimate application, causing it to load malicious code
- This allows the attacker to manipulate application behavior or execute unauthorized payloads

### Detection Suggestions
- Monitor the creation of shim database files (.sdb) using tools like Sysmon
- Alert on new shim configurations in non-standard locations

## Example 9: Netsh Helper DLL (T1546.007)

Attackers load a malicious helper DLL into the Netsh utility for execution and persistence.

### Command to Simulate Netsh Helper DLL Injection
```bash
operator-cli run-technique --technique T1546.007
```

### Example Behavior
- A malicious helper DLL is loaded into Netsh to intercept and execute attacker commands
- This technique provides a stealthy method for executing payloads

### Detection Suggestions
- Monitor Netsh usage for suspicious helper DLL configurations
- Validate loaded DLLs against known legitimate libraries

## Post-Simulation Validation

After running these simulations, ensure the following:

- Alerts are generated in your SIEM or EDR tools for each persistence method
- Logs capture critical details, such as file paths, registry keys, task names, or scripts
- Incident response teams validate the detection rules and refine them if necessary

## Commands Summary

| Technique | Command |
|-----------|---------|
| Scheduled Task Creation | `operator-cli run-technique --technique T1053.005` |
| Registry Persistence | `operator-cli run-technique --technique T1547.001` |
| Service Creation | `operator-cli run-technique --technique T1543.003` |
| DLL Hijacking | `operator-cli run-technique --technique T1574.001` |
| Logon Script Persistence | `operator-cli run-technique --technique T1037.001` |
| Office Add-In Execution | `operator-cli run-technique --technique T1137.001` |
| Boot Configuration Modification | `operator-cli run-technique --technique T1542.001` |
| Application Shimming | `operator-cli run-technique --technique T1546.011` |
| Netsh Helper DLL | `operator-cli run-technique --technique T1546.007` |

## Learn More

For more details on these persistence techniques, explore the relevant MITRE ATT&CK pages:

- [T1053.005: Scheduled Task/Job](https://attack.mitre.org/techniques/T1053/005/)
- [T1547.001: Registry Run Keys/Startup Folder](https://attack.mitre.org/techniques/T1547/001/)
- [T1543.003: Create or Modify System Process](https://attack.mitre.org/techniques/T1543/003/)
- [T1574.001: DLL Search Order Hijacking](https://attack.mitre.org/techniques/T1574/001/)
- [T1037.001: Boot or Logon Initialization Scripts](https://attack.mitre.org/techniques/T1037/001/)
- [T1137.001: Office Application Startup](https://attack.mitre.org/techniques/T1137/001/)
- [T1542.001: System Boot Configuration](https://attack.mitre.org/techniques/T1542/001/)
- [T1546.011: Application Shimming](https://attack.mitre.org/techniques/T1546/011/)
- [T1546.007: Netsh Helper DLL](https://attack.mitre.org/techniques/T1546/007/)
