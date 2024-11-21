Persistence Techniques Examples with Prelude Operator

Persistence techniques allow attackers to maintain access to a compromised system even after reboots or credential changes. This document demonstrates how to simulate persistence mechanisms using Prelude Operator to test and validate detection capabilities.
Example 1: Scheduled Tasks (T1053.005)

Attackers often use scheduled tasks to execute malicious payloads at specific intervals.
Command to Simulate Scheduled Task Creation

operator-cli run-technique --technique T1053.005

Example Behavior

    A scheduled task named ExampleTask is created to run a payload at a specific time.
    The task ensures that the payload is executed periodically or on a defined schedule.

Detection Suggestions

    Monitor for commands invoking schtasks.exe or Task Scheduler.
    Alert on task names or schedules created by unauthorized users.

Example 2: Registry Run Keys/Startup Folder (T1547.001)

Attackers use registry entries or the startup folder to automatically launch malicious programs on system startup.
Command to Simulate Registry Persistence

operator-cli run-technique --technique T1547.001

Example Behavior

    A registry key is added to the HKCU\Software\Microsoft\Windows\CurrentVersion\Run path.
    The key points to a malicious executable stored in %TEMP%\malware.exe.

Detection Suggestions

    Monitor for changes in the HKCU\Software\Microsoft\Windows\CurrentVersion\Run registry path.
    Alert on binaries being added to startup directories.

Example 3: Service Creation (T1543.003)

Attackers may create malicious services to execute unauthorized processes at boot.
Command to Simulate Service Creation

operator-cli run-technique --technique T1543.003

Example Behavior

    A new service named MaliciousService is created to execute malware.exe.
    Malicious services often mimic legitimate processes to evade detection.

Detection Suggestions

    Monitor service creation events in logs.
    Validate service binary paths against known system directories.

Example 4: DLL Hijacking (T1574.001)

Attackers place malicious DLLs in directories prioritized by the operating system’s search order to hijack legitimate processes.
Command to Simulate DLL Hijacking

operator-cli run-technique --technique T1574.001

Example Behavior

    A malicious DLL named example.dll is placed in a directory higher in the search order.
    When the application loads, it uses the attacker-controlled DLL instead of the legitimate one.

Detection Suggestions

    Monitor for changes in application-critical directories.
    Alert on DLL files with unexpected paths or names.

Example 5: Boot/Logon Scripts (T1037.001)

Malicious initialization scripts can execute commands or malware during system boot or user login.
Command to Simulate Logon Script Persistence

operator-cli run-technique --technique T1037.001

Example Behavior

    A script is placed in the startup folder or logon configuration to execute during user login.
    This ensures the attacker’s code is executed with every logon.

Detection Suggestions

    Monitor changes to the startup folder (C:\Users\[User]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup).
    Alert on unusual or unauthorized script files in these directories.

Example 6: Office Add-In Persistence (T1137.001)

Attackers can use malicious add-ins for Office applications like Word and Excel to execute unauthorized code.
Command to Simulate Office Add-In Execution

operator-cli run-technique --technique T1137.001

Example Behavior

    A malicious add-in file is placed in %APPDATA%\Microsoft\Word\STARTUP or %APPDATA%\Microsoft\Excel\XLSTART.
    The add-in executes attacker-controlled code whenever the application is opened.

Detection Suggestions

    Monitor Office add-in directories for new or modified files.
    Validate DLL or script files against known legitimate add-ins.

Example 7: System Boot Configuration Modification (T1542.001)

Attackers modify system boot configurations to execute malicious code early in the boot process.
Command to Simulate Boot Configuration Modification

operator-cli run-technique --technique T1542.001

Example Behavior

    The boot configuration data (BCD) is altered to include a malicious driver or application.
    This ensures that the payload executes early during system initialization.

Detection Suggestions

    Monitor changes to the boot configuration using commands like bcdedit.
    Alert on unauthorized modifications to boot-critical files or settings.

Example 8: Application Shimming (T1546.011)

Attackers create custom shims to intercept and modify application behavior for persistence.
Command to Simulate Application Shimming

operator-cli run-technique --technique T1546.011

Example Behavior

    A custom shim is created for a legitimate application, causing it to load malicious code.
    This allows the attacker to manipulate application behavior or execute unauthorized payloads.

Detection Suggestions

    Monitor the creation of shim database files (.sdb) using tools like Sysmon.
    Alert on new shim configurations in non-standard locations.

Example 9: Netsh Helper DLL (T1546.007)

Attackers load a malicious helper DLL into the Netsh utility for execution and persistence.
Command to Simulate Netsh Helper DLL Injection

operator-cli run-technique --technique T1546.007

Example Behavior

    A malicious helper DLL is loaded into Netsh to intercept and execute attacker commands.
    This technique provides a stealthy method for executing payloads.

Detection Suggestions

    Monitor Netsh usage for suspicious helper DLL configurations.
    Validate loaded DLLs against known legitimate libraries.

Post-Simulation Validation

After running these simulations:

    Ensure alerts are generated in your SIEM or EDR tools for each persistence method.
    Verify that log entries capture key details like file paths, registry keys, or task names.
    Update detection rules and correlate findings to refine your defensive strategies.

Learn More

Explore the full details of these techniques on MITRE ATT&CK:

    T1053.005: Scheduled Task/Job
    T1547.001: Registry Run Keys/Startup Folder
    T1543.003: Windows Service
    T1574.001: DLL Search Order Hijacking
    T1037.001: Logon Script (Windows)
    T1137.001: Office Template Macros
    T1542.001: System Firmware
    T1546.011: Application Shimming
    T1546.007: Netsh Helper DLL
