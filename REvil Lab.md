1. To begin your investigation, can you identify the filename of the note that the ransomware left behind?

index=revil event.code="11"
| stats values(winlog.event_data.TargetFilename)
-> see file 5uizv5660t-readme.txt were created in many directory (eventID 11 : file create)

2. After identifying the ransom note, the next step is to pinpoint the source. What's the process ID of the ransomware that's likely involved

index=revil winlog.event_data.TargetFilename="*5uizv5660t-readme.txt*"
| stats values(winlog.event_data.ProcessId)

3. Having determined the ransomware's process ID, the next logical step is to locate its origin. Where can we find the ransomware's executable file?

index=revil "event.code"=1 winlog.event_data.ProcessId="5348" "winlog.event_data.RuleName"="technique_id=T1204,technique_name=User Execution"
| table winlog.event_data.CommandLine

-> search eventID là 1 (process create) có nghĩa là khi 1 process được chạy thì file ransomware mới được tạo ra từ parent process và chil process sẽ là processID 5348 với eventID là 11 (file create) có 2 RuleName được bắt thì chọn ruleName liên quan tới user execution

4. Now that you've pinpointed the ransomware's executable location, let's dig deeper. It's a common tactic for ransomware to disrupt system recovery methods. Can you identify the command that was used for this purpose?

search with parent là facebook assistant.exe lấy kết quả command line
-> index=revil "winlog.event_data.ParentImage"="C:\\Users\\Administrator\\Downloads\\facebook assistant.exe"
| table winlog.event_data.CommandLine
-> result: powershell -e RwBlAHQALQBXAG0AaQBPAGIAagBlAGMAdAAgAFcAaQBuADMAMgBfAFMAaABhAGQAbwB3AGMAbwBwAHkAIAB8ACAARgBvAHIARQBhAGMAaAAtAE8AYgBqAGUAYwB0ACAAewAkAF8ALgBEAGUAbABlAHQAZQAoACkAOwB9AA==
-> decode base64: powershell -e "Get-WmiObject Win32_Shadowcopy | ForEach-Object {$_.Delete();}"

5. As we trace the ransomware's steps, a deeper verification is needed. Can you provide the sha256 hash of the ransomware's executable to cross-check with known malicious signatures?

index=revil (winlog.event_id="11" OR winlog.event_id="1") winlog.event_data.Hashes!=""
| stats values(winlog.event_data.Hashes)



