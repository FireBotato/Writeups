![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/ca63f052-7602-4a40-b14c-06b4e27f74bb)

we are given a pcap file and asked for the root password
The description mentioned that it's kinda of camera hacking , so first thing i went looking for the type/version of this camera
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/870443a8-a4c1-44e1-9e0e-a9295eb3e22d)

so googling about this camera , i found this CVE

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/cb27693e-ea7e-4a3b-840c-7d69d93bdac1)

where this tool needed the config file for that camera , so coming back to the pcap
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/bce5e7cf-518b-476b-ad8c-13824975abc0)

running the tool in the config file we find the password
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/5b7dde0d-e08a-4671-8cad-3dc41f1813d4)

so the flag was METACTF{deadF00F420}
