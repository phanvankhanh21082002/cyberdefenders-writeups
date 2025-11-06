1. Identifying an attacker's IP address is crucial for mapping the attack's extent and planning an effective response. What is the attacker's IP address?

=> Statistics -> Conversations -> IPv4 -> Src: 111.224.180.128, Dst: 73.124.17.52 , Packets: 14.517 packet

2. The attacker used a directory brute-forcing tool to discover hidden paths. Which tool did the attacker use to perform the brute-forcing?

ip.src == 111.224.180.128 && http
=> Click 1 packet of HTTP request => Right click of User agent => "Apply as Column" 
=> See User-agent: gobuster/3.6

3. Cross-Site Scripting (XSS) allows attackers to inject malicious scripts into web pages viewed by users. Can you specify the XSS payload that the attacker used to compromise the integrity of the web application?

ip.src == 111.224.180.128 && http.request.method == "POST"
=> Packet of "10058" is XSS injection attack at 2024-03-29 12:08:47

4. Pinpointing the exact moment an admin user encounters the injected malicious script is crucial for understanding the timeline of a security breach. Can you provide the UTC timestamp when the admin user first visited the page containing the injected malicious script?

=> Search Src_IP != 111.224.180.128
=> ip.src != 111.224.180.128 && http
=> Packet 10078 => GET /admin/log_viewer.php?file=error.log HTTP/1.1\r\n at 2024-03-29 12:09
=> Cookie of admin session: PHPSESSID=lqkctf24s9h9lg67teu8uevn3q

5. The theft of a session token through XSS is a serious security breach that allows unauthorized access. Can you provide the session token that the attacker acquired and used for this unauthorized access?
=> Packet 10078 => GET /admin/log_viewer.php?file=error.log HTTP/1.1\r\n at 2024-03-29 12:09
=> Cookie of admin session: PHPSESSID=lqkctf24s9h9lg67teu8uevn3q

6. Identifying which scripts have been exploited is crucial for mitigating vulnerabilities in a web application. What is the name of the script that was exploited by the attacker?

ip.src == 111.224.180.128 && http
=> Packet "10205" and "10217" 
=> Attacker use cookie "lqkctf24s9h9lg67teu8uevn3q" of admin and query with parameter "file" at "/admin/log_viewer.php"

7. Exploiting vulnerabilities to access sensitive system files is a common tactic used by attackers. Can you identify the specific payload the attacker used to access a sensitive system file?

=> Packet "10217" see path traversal attack: "GET /admin/log_viewer.php?file=../../../../../etc/passwd HTTP/1.1\r\n"





