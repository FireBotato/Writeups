![Divine REVENGE](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/bb27621a-9629-4a09-9e9d-5f100325ece6)
here we are given a disk image ,i found a deleted 7z file , but it was password protected
my first guess was saved browser in edge , but no luck 
after that i saw the RDP cahce
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/60141ca9-8ea9-4f8c-b22e-87b6e04d5fbe)

having a tool that can extract the last live rdp image 
`https://github.com/ANSSI-FR/bmc-tools/`
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/f9c4931f-0422-4351-9089-89055fcec3b9)

now we have the images , but we need a tool to bring them togther so we can see the image clearly , so i used this tool 
https://github.com/BSI-Bund/RdpCacheStitcher/releases/tag/v1.1

putting the images we found the password
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/fa7faec0-ae0f-473a-8221-22ec5a608182)

after unzipping the file we find registery logs
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/9068f7a1-778f-428b-9f7c-723a89e40ae9)

going to software via registry explorer --> to the run key (my first check always)
i find out that the attacker tries to make a run key that runs everytime the systems boots
it is an encoded base64 powershell command that this command calls from the key given in the command
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/7f922c70-c339-4b46-b815-ec40bbb1f440)

going to that key, i found the base64 command
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/295bc701-6e10-46e8-810f-dce81a4a4dd9)

decoing it
we can see base64 commented
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/682e9fa3-ff48-48a2-8dd3-bec3ec2d4c9c)

after that decoing the commented base64
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/df3b4253-2206-45ea-b700-c694b68b26d5)

the flag :METACTF{y0u_f0UnD_TrU3_D1V1nItY_y0u_ShoulD_Bec0m3_a_M4lw4r3_An4lYSt}

creds:https://medium.com/@ronald.craft/blind-forensics-with-the-rdp-bitmap-cache-16e0c202f91c
