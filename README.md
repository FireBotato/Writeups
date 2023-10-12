# Writeups
Forensics challenges from BlackHat MEA CTF Qualifications 2023 
<br>
## *USB100* (Easy - 50 points) <br>
After downloading the challenge files and unzipping them using the password "flagyard", you can find the pcapng file "send.pcapng" <br> <br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/0556405f-5fa6-4eb3-8b70-4042e48b8051) <br> <br>
Firstly, I tried to open it with Wireshark for a bit and try to analyze it but it got me nowhere, so I used Binwalk to see the files stored inside of it and look what came up <br> <br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/424e7270-998e-48e6-a393-5141eb0422e2) <br> <br>
As you can see from the photo there is a Microsoft executable with a hexadecimal of *AC723* stored inside so we need to extract it, by using the command <br>
`binwalk -e --dd=".*" send.pcapng`
<br> <br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/d99af396-2b94-4aab-8efa-00228b712521) <br> <br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/8f62f711-7f12-49f3-8a3b-88d9c6c9cc2d)<br><br>
After getting this file you can copy it to a Windows operating system machine and therefore execute it to find this flag: <br> <br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/9b7d4f29-2343-4beb-8b80-91a2deb4f1d0)


