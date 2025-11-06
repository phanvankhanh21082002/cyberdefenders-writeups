1. Identifying the attacker's IP address helps trace the source and stop further attacks. What is the attacker's IP address?
-> Base on the scenario "allowing them to upload webshells and gain full control over the system. The attacker utilized the compromised web server as a launch point for further malicious activities, including data manipulation." 
-> search http.request.method == POST and see payload "http://3.71.79.4:8111/admin/pluginUpload.html" from IP "23.158.56.196"

2. To identify potential vulnerability exploitation, what version of our web server service is running?
-> Follow HTTP stream of packet "24825" in see version in response detail of packet

3. After identifying the version of our web server service, what CVE number corresponds to the vulnerability the attacker exploited?
5. The attacker uploaded a webshell to ensure his access to the system. What is the name of the file that the attacker uploaded?

->  Follo TCP stream of packet "25371" and see the code
"NSt8bHTg.zip
--018dbf95280c614c179495e8463dea18
Content-Disposition: form-data; name="file:fileToUpload"; filename="NSt8bHTg.zip"
Content-Type: application/zip "

-> search in chatgpt to define CVE

4. The attacker exploited the vulnerability to create a user account. What credentials did he set up?

http.request.method == POST && ip.src == 23.158.56.196
-> see packet "24721" 

6. When did the attacker execute their first command via the web shell?
7. The attacker tampered with a text file that contained the credentials of the admin user of the webserver. What new username and password did the attacker write in the file?
8. What is the MITRE Technique ID for the attacker's action in the previous question (Q7) when tampering with the text file?
9. The attacker tried to escape from the container but he didn’t succeed, What is the command that he used for that?

http.request.method == POST && ip.src == 23.158.56.196
-> see packet "25572" . Click View -> Time Display Format -> UTC Date and Time Format
-> see packet "31123" and see Command in HTML form "bash -c 'echo "username:a1l4m,password:youarecompromised" > /tmp/Creds.txt'"
-> Search in chatgpt => T1565.001 — Stored Data Manipulation
-> see packet "32111" with CMD: "docker run --rm -it -v /:/host ubuntu chroot /host"