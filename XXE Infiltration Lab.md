1. Identifying the open ports discovered by an attacker helps us understand which services are exposed and potentially vulnerable. Can you identify the highest-numbered port that is open on the victim's web server?

Click Statistics -> Conversations -> TCP and see many request from IP "210.106.114.183" and see port 3306 (port indicate to mysql) => 3306

2. By identifying the vulnerable PHP script, security teams can directly address and mitigate the vulnerability. What's the complete URI of the PHP script vulnerable to XXE Injection?
3. To construct the attack timeline and determine the initial point of compromise. What's the name of the first malicious XML file uploaded by the attacker?

ip.src == 210.106.114.183 && http.request.method == "POST"
-> TCP stream of packet "88306" and see the XXE injection
-> file "TheGreatGatsby.xml" were uploaded by the attacker

4. Understanding which sensitive files were accessed helps evaluate the breach's potential impact. What's the name of the web app configuration file the attacker read?
5. To assess the scope of the breach, what is the password for the compromised database user?

-> Follow TCP stream with stream "10462" and see file "file:///var/www/html/config.php" and password

6. Following the database user compromise. What is the timestamp of the attacker's initial connection to the MySQL server using the compromised credentials after the exposure?

ip.src == 210.106.114.183 && mysql
-> See packet "88348" attacker access mysql after have credential

7. To eliminate the threat and prevent further unauthorized access, can you identify the name of the web shell that the attacker uploaded for remote code execution and persistence?

ip.src == 210.106.114.183 && http
-> See path "/uploads/booking.php?cmd=" with parameter "cmd" and insert the command like "ls" ,"whoami"












