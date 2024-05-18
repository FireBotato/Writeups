![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/30d44f37-9d81-4ca8-865c-e27473a81527)

so here we are given another pcap and we want to see what did the attacker exfiltrate from the comrpomsied machine

Firstly what caught my eyes initating a variable in powershell
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/b967fbbc-1295-48c5-aefc-6a784e7198ff)

so trying to extract all the powersehll script by using this command
` tshark -r SupremeTheftData.pcapng -T fields -e data.data -Y "data.len==512" `
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/c0af8c9f-8cf2-4bb4-9181-d8986ad79797)

we can see the powershell command but it's missing something

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/18783d83-e093-447f-be87-ff324f6af5bc)

went back to the pcap and found the missing part
so as you can see the first code highlighted reverses the base64 string and second one decode it
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/4bafdcdb-93d9-4fb6-8cbe-6497b1e667a8)

we get a very long powershell command
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/d7eaea9f-ca82-42d0-bb36-06de20c91f73)

all of them had comments (chatgpt maded) , but one of them was obv that was custom 
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/a8dca41a-08a3-4640-83ae-a4e092661d24)

we found a base64 encoded password , but for what?
coming back to the pcap , we can see that the attacker tries to send multiple files one of them had 7z header 
so extracting it using the command 
`tshark -r SupremeTheftData.pcapng -T fields -e data.data   > hex.txt`
we get our 7zip --> now we decode the password we got from the powershell script and use it as password for the 7z found 
we get a pdf
i have already cracked the pdf but the command used 
`pdf2john <pdf> > hash.txt`
then
`john --wordlist=/usr/share/wordlists/rockyou.txt'
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/49d43b58-9496-4b28-be82-cc01845c6c3f)

opening the pdf
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/44408bde-35c1-42ad-8e93-6629ccebda4e)

the flag : METACTF{Dragon_Ball_Sparking!_Zero_is_
Releasing_in_2024!!}



