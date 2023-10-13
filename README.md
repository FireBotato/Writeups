# Writeups <br>

## Forensics challenges from BlackHat MEA CTF Qualifications 2023 
### *USB100* (Easy - 50 points) <br>
Challenge Description: In a shocking turn of events, a malicious actor managed to gain physical access to our victim's computer by plugging in a rogue USB device. As a result, all critical data has been pilfered from the system. Flag is direct without BHFlagY{} tag.
<br>
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
<br><br> <br> <br>
### Not supported (Medium - 150 points) <br>
Challenge Description: Straight forward challenge, the flag is written on running notepad process. Flag is direct without BHFlagY{} tag. <br> <br>

When you first download the file in this challenge and extract it, there's a file with the link to download a memdump.mem file <br> <br>
As the challenge description mentions, we know that this file is a capture of a RAM memory that was running on a computer and we need to find what was written on the notepad process. <br><br>
So the first thing I did was use volatility3 to extract the process information using the command <br>
`vol.py -f “/path/to/file” windows.pslist` <br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/b715ecfa-45e6-4cda-b66c-23074751cc03)
<br>
Scrolling down you can see the process "Notepad.exe" with the PID of (6028)<br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/8232b9a0-c2e3-40e1-b34c-ec2224d01ad9)
<br>
The next step was to memory dump the process so then you can search through the text for the flag <br>
to memory dump the process I used the command <br>
`vol.py -f “/path/to/file” -o “/path/to/dir” windows.memmap ‑‑dump ‑‑pid <PID>`<br>
with the PID of 6028 <br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/4d62e734-91d5-4201-8394-393f0944c52a) <br>
After it finishes dumping the process you can navigate to the output file and run the `strings` command followed by the `grep` command searching for the flag format given by the challenge which was "bhflagy", and I also used the `-B` and `-A` option to include lines before and after the text was found. So the final command was: <br>
`strings pid.6028.dmp | grep -i "bhflagy" -B 5 -A 5`<br>
![image](https://github.com/FireBotato/Writeups/assets/114668318/9fe2d743-28b8-402b-b4f8-408d0f4c7bc3)<br>
the last step was to remove the spaces found and submit the flag <br> <br> <br>






