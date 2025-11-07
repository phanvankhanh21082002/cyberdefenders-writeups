1. In the memory dump analysis, determining the root of the malicious activity is essential for comprehending the extent of the intrusion. What is the name of the parent process that triggered this malicious behavior?
2. Once the rogue process is identified, its exact location on the device can reveal more about its nature and source. Where is this process housed on the workstation?
6. Once retrieved, the malware aims to activate its additional components. Which child process is initiated by the malware to execute these files?

=> python3 ../Tools/volatility3/vol.py -f file.vmem windows.pstree
=> python3 ../Tools/volatility3/vol.py -f file.vmem windows.cmdline
=> See 2748	2524	lssass.exe	0xfa800300a750	7	254	1	True	2023-08-09 21:33:04.000000 	N/A
       3064	2748	rundll32.exe	0xfa8003042b30	1	64	1	True	2023-08-09 21:33:56.000000 	N/A
=> 2748	lssass.exe	"C:\Users\0XSH3R~1\AppData\Local\Temp\925e7e99c5\lssass.exe" 
   3064	rundll32.exe	"C:\Windows\System32\rundll32.exe" C:\Users\0xSh3rl0ck\AppData\Roaming\116711e5a2ab05\clip64.dll, Main
=> malcious process: rundll32.exe and parent process: lssass.exe

3. Persistent external communications suggest the malware's attempts to reach out C2C server. Can you identify the Command and Control (C2C) server IP that the process interacts with?

=> python3 ../Tools/volatility3/vol.py -o extract/ -f file.vmem windows.dumpfiles --pid 2748
=> strings extract | grep -ir "http*/"
=> http[:]//41.75.84.12/rock/Plugins/clip64.dll
=> http[:]//41.75.84.12/rock/index.php
=> C2C server: 41.75.84.12

4. Following the malware link with the C2C, the malware is likely fetching additional tools or modules. How many distinct files is it trying to bring onto the compromised workstation?
=> clip64.dll, index.php

5. Identifying the storage points of these additional components is critical for containment and cleanup. What is the full path of the file downloaded and used by the malware in its malicious activity?
=> python3 ../Tools/volatility3/vol.py -f file.vmem windows.filescan
=> search clip64.dll

7. Understanding the full range of Amadey's persistence mechanisms can help in an effective mitigation. Apart from the locations already spotlighted, where else might the malware be ensuring its consistent presence?

=> python3 ../Tools/volatility3/vol.py -f file.vmem windows.filescan
=> search lssass.exe => \Windows\System32\Tasks\lssass.exe









 