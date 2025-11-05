1. During the investigation of network traffic, unusual patterns of activity were observed in Suricata logs, suggesting potential unauthorized access. One external IP address initiated access attempts and was later seen downloading a suspicious executable file. This activity strongly indicates the origin of the attack.
What is the IP address from which the initial unauthorized access originated?

2. Investigating the attacker’s domain helps identify the infrastructure used for the attack, assess its connections to other threats, and take measures to mitigate future attacks. What is the domain name of the attacker server?

3. Knowing the IP address of the targeted system helps focus remediation efforts and assess the extent of the compromise. What is the IP address of the system that was targeted in this breach?

index=suricata_ids "http.http_method"=GET "http.http_user_agent"=Download http_content_type="text/plain" files{}.filename!=""
| dedup src_ip http.hostname dest_ip
| table src_ip http.hostname dest_ip

4. Identify all the unique files downloaded to the compromised host. How many of these files could potentially be malicious? 

index=suricata_ids "http.http_method"=GET src_ip="195.88.191.59" dest_ip="147.32.84.165"
| stats values(filename) , dc(filename) 

5. What is the SHA256 hash of the malicious file disguised as a .txt file?

file .txt time 09:06 and 10:10

index=* "195.88.191.59" "147.32.84.165" sourcetype="zeek:files"
| stats values(md5) -> get md5 at 09:06 and 10:10 and search in virustotal get sha256