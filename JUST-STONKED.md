We were given an MFT file
Where the challenge mentioned that someone played with your laptop and you work on a stock company , figure out which stock got changed, the stomped time , last access time
so first , what is Stompped time?
Stompped time is an anti-foreniscs techqinue that makes the Job Harder for Digital Forensics investigator to know the correct timestamp
so im MFT Parser we can see that it shows FileName information (FN) and 

![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/ec48e391-47bf-49ce-8c9a-f0946642d4b5)

refer to this article
`https://az4n6.blogspot.com/2014/10/timestomp-mft-shenanigans.html` 

so running MFTExplorer
first we need to identify which stock got modified and it is WIX
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/b67052b1-1909-444d-bbb7-c95b5b5a61cf)

after that we need to see last time access and Stompped Time
![image](https://github.com/CMDJO-QAIS/CTF-Writeups/assets/160439920/148c573d-dde4-4e3a-9300-ca4ff563cb8d)

so the flag is
JUST{WIX_14/05/2024-12:10:04.7590217_14/05/2024-12:33:41.6359035}
