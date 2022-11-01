202210252205
Status:: #ctf
Tags:

# hack_the_boo_trick_or_breach
Platform: *hackthebox*
event: *hack the boo*
type: *forensics*
task: *Our company has been working on a secret project for almost a year. None knows about the subject, although rumor is that it is about an old Halloween legend where an old witch in the woods invented a potion to bring pumpkins to life, but in a more up-to-date approach. Unfortunately, we learned that malicious actors accessed our network in a massive cyber attack. Our security team found that the hack had occurred when a group of children came into the office's security external room for trick or treat. One of the children was found to be a paid actor and managed to insert a USB into one of the security personnel's computers, which allowed the hackers to gain access to the company's systems. We only have a network capture during the time of the incident. Can you find out if they stole the secret project?*
flag: **HTB{M4g1c_c4nn0t_pr3v3nt_d4t4_br34ch}**

# steps
In this pcap file we are met by an dns exfiltration requests.

Extracting urls:
`tshark -r capture.pcap -T fields  -e dns.qry.name -Y "dns.flags.response eq 0" > urls.txt`

Result:
```bash
tshark -r capture.pcap -T fields  -e dns.qry.name -Y "dns.flags.response eq 0" | cut -d  '.' -f1 | tr -d "\n\r" > data.hex
```

Create binary file from hexdump:
`xxd -r -p data.hex data.bin `                                                                           


```bash
file data.bin                                                                                           
data.bin: Microsoft Excel 2007+
```

After opening file in spreadsheet editor, we get the flag:
![[Pasted image 20221025230828.png]]