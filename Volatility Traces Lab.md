1. Identifying the parent process reveals the source and potential additional malicious activity. What is the name of the suspicious process that spawned two malicious PowerShell processes?

python3 vol.py -f "/home/ubuntu/Desktop/Start here/Artifacts/memory.dmp" windows.pstree
-> 6980	4596	powershell.exe	0xb882f10e9080	13	-	1	True	2024-05-02 06:57:59.000000 	N/A	
Add-MpPreference -ExclusionPath "C:\Users\Lee\AppData\Local\Temp\InvoiceCheckList.exe
-> file InvoiceCheckList.exe were Add-MpPreference -ExclusionPath to avoid scan of AV scan

2. By determining which executable is utilized by the malware to ensure its persistence, we can strategize for the eradication phase. Which executable is responsible for the malware's persistence?

python3 vol.py -f "/home/ubuntu/Desktop/Start here/Artifacts/memory.dmp" windows.psscan
-> 4596	3800 InvoiceCheckList.exe -> PID: 4596 , PPID: 3800
-> find sub process were with PPID: 4596 -> 3512	4596	schtasks.exe 

3. Understanding child processes reveals potential malicious behavior in incidents. Aside from the PowerShell processes, what other active suspicious process, originating from the same parent process, is identified?
python3 vol.py -f "/home/ubuntu/Desktop/Start here/Artifacts/memory.dmp" windows.psscan
-> 4164	4596	RegSvcs.exe -> PID: 4164 , PPID: 4596 (InvoiceCheckList.exe)

4. Analyzing malicious process parameters uncovers intentions like defense evasion for hidden, stealthy malware. What PowerShell cmdlet used by the malware for defense evasion?

python3 vol.py -f "/home/ubuntu/Desktop/Start here/Artifacts/memory.dmp" windows.pstree
-> 6980	4596	powershell.exe	0xb882f10e9080	13	-	1	True	2024-05-02 06:57:59.000000 	N/A	 Add-MpPreference -ExclusionPath 
=> Add-MpPreference

5. Recognizing detection-evasive executables is crucial for monitoring their harmful and malicious system activities. Which two applications were excluded by the malware from the previously altered application's settings?

python3 vol.py -f "/home/ubuntu/Desktop/Start here/Artifacts/memory.dmp" windows.pstree
=> 6980	4596 "C:\Users\Lee\AppData\Local\Temp\InvoiceCheckList.exe"
=> 7656	4596 "C:\Users\Lee\AppData\Roaming\HcdmIYYf.exe"

=> InvoiceCheckList.exe , HcdmIYYf.exe

6. What is the specific MITRE sub-technique ID associated with PowerShell commands that aim to disable or modify antivirus settings to evade detection during incident analysis?

=> Add-MpPreference -ExclusionPath : T1562.001

7. Determining the user account offers valuable information about its privileges, whether it is domain-based or local, and its potential involvement in malicious activities. Which user account is linked to the malicious processes?

=> C:\Users\Lee\AppData\Roaming\ => User: Lee








