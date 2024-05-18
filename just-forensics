so in this challenge we were given a disk image and a pcap file , and the file asked about 4 questions
1.how many open ports does the compromised service has?
2.what cve did the attacker abuse?
3.the attacker dropped a file in the compromised server, what is the md5 hash for this file?
4.the attacker exfiltirated a file , what is the content of that file?
Firstly , the open port identifying the comrpised service ip --> 192.168.247.130
so filtering for that ip and tcp.flag=0x12

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/d52c0cb4-0636-4dc9-adbb-a862d196015f)

** tcp.flag=0x12 --> 3 handway shake happened successfuly --> so the port is open**

so the first question answer was 3 ports

for the second one
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/134a9b56-87d2-43dd-a700-91d032c3dc41)

we can see that the attacker has successfully got a shell via /cgi/spaceship.bat , so its kinda of a web service (Tomcat) looking for it's version in the pcap


![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/c45cbf8a-e895-4e7c-87b0-086d81c8872b)

googling about it's CVE

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/1f7b78dd-4396-4141-9eb0-7b9d7dfe4aa6)

so the answer for this question is CVE-2019-0232

For the third question we check the pcap once again
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/2802b3ce-a038-403f-8387-779c10fb31f8)

we can see that the attacker dropped a executable called reverseshell.exe

going to the disk now
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/e5c5772e-891a-46ce-955d-8f2becdbb623)

getting the hash of the file --> a3b025d51f82d6f69f9970a9e2d1b397

so for the last question (The Only Hard Question)
in the pcap we find the python script that the attacker used to exfiltrate the data
we can see that the attacker is Sending the data via ICMP bit by bit
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/a5a5f98b-4b72-4d6b-963c-c9b2c6924b81)

so we try to extract this data
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/3b2e3059-1700-4062-82ca-d3a0afd396dc)

this is the icmpv6 packets , so trying to remove responses and broken packets
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/56417f0d-7d28-41a1-8f0d-3b6592493c7c)

after filtering , we can see that the data is being exfiltirated by ipv6flow ( we say that in the script as well)
so trying to extract it
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/8f8f095d-e8db-4587-95d3-58aee9fc7e6a)

so we are not done here

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/f6143144-6f65-408c-b473-9d79bb7077c8)

the data seemed to be encrypted , we can see in the pcap the extension of the exfilitrated data is .cpt

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/542a5ed1-d925-42e0-a0ea-6878d844ebea)

checking the disk in the desktop of the user we can see an encryption/decryption software
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/068bb7f2-d950-4fe0-b743-d3f3ea331c49)

downloading it 
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/871422fe-14d9-489a-9c66-8249e8fc9845)

it asks for a password , so here i got stuck for a little bit , but i found this on his desktop
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/03a51e04-227a-42be-afe7-4ad4a88e54b7)

as you can see here it's a story on the user comrpoised , with some values bold , so custome wordlist?
tried to play with them but no luck , but after digging , i gound a tool called CCUP

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/800bc981-8942-42e9-8be2-f3e4eae0ef76)

it ask for all the values that was bolded , so in my mind i was like Bingo
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/d3ebffca-7a8b-4cfc-8152-5b8d51be8152)

now i have my wordlist , now lets try to run the file
running for loop on the file

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/de57e337-730c-4c58-b6f1-ee548ee4b03a)

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/92347b8e-f4bd-49ab-a1e7-ba2a01165912)

opening the decrypted file
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/c9c28e56-3dab-4d2b-8117-f9ff865f280f)

so the flag is 
JUST{3_CVE-2019-0232_a3b025d51f82d6f69f9970a9e2d1b397_1N_5P4C3_N0_0N3_C4N_H34r_Y0U_5Cr34M}
