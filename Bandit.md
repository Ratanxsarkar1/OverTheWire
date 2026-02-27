
---
# 🏴 OverTheWire Bandit Complete Write-up (Level 0 → 33) 
---
# 🔹 Level 0
### 🎯 Goal

Read the password from a file.

### 📘 Theory

Basic Linux file reading using:

- `ls` → list files
- `cat` → display file content

### 🛠 Walkthrough

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls
cat readme
```

Password found inside `readme`.

<details>
<summary><b>Password</b></summary>
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
</details>
 ---
# 🔹 Level 1

### 🎯 Goal

Read a file named `-`

### 📘 Theory

Files starting with `-` are treated as options by commands.

Solution:

- Use `./-`
- Or use `--` to stop option parsing
### 🛠 Walkthrough

```bash
ls -la
cat ./-
```

<details> <summary><b>Password</b></summary>  263JGJPfgU6LtdEvgfWU1XP5yac29mFx  </details> 

---
# 🔹 Level 2

### 🎯 Goal

Read file with spaces in name.

### 📘 Theory

Spaces break arguments in Linux.  
Solutions:

- Escape spaces with `\`
- Or use quotes

### 🛠 Walkthrough

```bash
ls
cat ./--spaces\ in\ this\ filename--
```

<details> <summary><b>Password</b></summary>  MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx  </details>

---

# 🔹 Level 3

### 🎯 Goal

Find hidden file.

### 📘 Theory

Files starting with `.` are hidden.

Use:
```bash
ls -la
```

### 🛠 Walkthrough

```bash
cd inhere
ls -la
cat ...Hiding-From-You
```


<details> <summary><b>Password</b></summary>   2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ </details>

---
# 🔹 Level 4

### 🎯 Goal

Find human-readable file.

### 📘 Theory

Use `file` command to detect file type.

### 🛠 Walkthrough

```bash
file ./*
```

Only one ASCII file:

```bash
cat ./-file07
```

<details> <summary><b>Password</b></summary>  4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw  </details>

---

# 🔹 Level 5

### 🎯 Goal

Find file:

- size 1033 bytes
- not executable

### 📘 Theory

Use `find` with:

- `-type`
- `-size`
- `! -executable`

### 🛠 Walkthrough

```bash
find . -type f -size 1033c ! -executable
cat maybehere07/.file2
```

<details> <summary><b>Password</b></summary>  HWasnPhtq9AVKe0dmk45nxy20cvUa6EG  </details>

---

# 🔹 Level 6

### 🎯 Goal

Find file:

- owned by bandit7
- group bandit6
- size 33 bytes

### 📘 Theory

Search entire filesystem.  
Suppress errors:

```bash
2>/dev/null
```

### 🛠 Walkthrough

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

<details> <summary><b>Password</b></summary>  morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj  </details>

---

# 🔹 Level 7

### 🎯 Goal

Find line containing "millionth".

### 📘 Theory

`grep` searches inside files.

### 🛠 Walkthrough

```bash
grep millionth data.txt
```

<details> <summary><b>Password</b></summary>  dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc  </details>

---

# 🔹 Level 8

### 🎯 Goal

Find unique line.

### 📘 Theory

- `sort`
- `uniq -u` → show unique lines

### 🛠 Walkthrough

```bash
sort data.txt | uniq -u
```

<details> <summary><b>Password</b></summary>  4CKMh1JI91bUIZZPXDqGanal4xvAg0JM  </details>

---

# 🔹 Level 9

### 🎯 Goal

Find readable strings inside binary.

### 📘 Theory

`strings` extracts printable characters.

### 🛠 Walkthrough

```bash
strings data.txt | grep =
```

<details> <summary><b>Password</b></summary>  FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey  </details>

---

# 🔹 Level 10

### 🎯 Goal

Decode Base64 string.

### 📘 Theory

Base64 encoding:

```bash
base64 -d
```

### 🛠 Walkthrough

```bash
strings data.txt
echo "<encoded>" | base64 -d
```

<details> <summary><b>Password</b></summary>  dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr  </details>

---

# 🔹 Level 11

### 🎯 Goal

Decode ROT13 text.

### 📘 Theory

ROT13 shifts letters by 13.

Use:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### 🛠 Walkthrough

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

<details> <summary><b>Password</b></summary>  7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4  </details>

---

# 🔹 Level 12

### 🎯 Goal

Multi-layer compression.

### 📘 Theory

Identify file type repeatedly using:

- `file`
- `gunzip`
- `bunzip2`
- `tar -xf`
- `xxd -r`

### 🛠 Walkthrough Strategy

1. Convert hex → binary
2. Check file type
3. Decompress
4. Repeat until ASCII

Finally:

```bash
cat data
```

<details> <summary><b>Password</b></summary>  FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn  </details>

---

# 🔹 Level 13

### 🎯 Goal

Use private SSH key.

### 📘 Theory

SSH with key:

```bash
ssh -i keyfile user@host
```

### 🛠 Walkthrough

```bash
cat sshkey.private > idrsa
chmod 600 idrsa
ssh -i idrsa bandit14@bandit.labs.overthewire.org -p 2220
```

<details> <summary><b>Password</b></summary>  MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS  </details>

---

# 🔹 Level 14

### 🎯 Goal

Connect to local port 30000.

### 📘 Theory

`nc` (netcat) connects to TCP ports.

### 🛠 Walkthrough

```bash
nc localhost 30000
```

Paste password.

<details> <summary><b>Password</b></summary>  8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo  </details>

---

# 🔹 Level 15

### 🎯 Goal

Connect using SSL.

### 📘 Theory

Use:

```bash
openssl s_client
```

### 🛠 Walkthrough

```bash
openssl s_client -connect localhost:30001
```

<details> <summary><b>Password</b></summary>  kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx  </details>

---

# 🔹 Level 16

### 🎯 Goal

Find correct SSL port.

### 📘 Theory

Use:

```bash
nmap -sV
```

### 🛠 Walkthrough

```bash
nmap -p 31000-32000 -sV localhost
openssl s_client -connect localhost:31790
```

<details> <summary><b>Password</b></summary>  -----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----  </details>

---

# 🔹 Level 17

### 🎯 Goal

Compare two files.

### 📘 Theory

`diff` shows difference.

### 🛠 Walkthrough

```bash
diff passwords.new passwords.old
```

<details> <summary><b>Password</b></summary>  x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO  </details>

---

# 🔹 Level 18

### 🎯 Goal

Bypass forced logout.

### 📘 Theory

Run command directly over SSH.

### 🛠 Walkthrough

```bash
ssh bandit18@... -p 2220 cat readme
```

<details> <summary><b>Password</b></summary>  cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8  </details>

--- 
# 🔹 Level 19

### 🎯 Goal

Exploit SUID binary.

### 📘 Theory

SUID → runs as file owner.

### 🛠 Walkthrough

```bash
./bandit20-do /bin/bash -p
cat /etc/bandit_pass/bandit20
```

 <details> <summary><b>Password</b></summary>  0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO  </details>

---
# 🔹 Level 20

### 🎯 Goal

Use listener for password validation.

### 📘 Theory

- `nc -lvp`
- Reverse communication

### 🛠 Walkthrough

Terminal 1:

```bash
nc -lvp 4444
```

Terminal 2:

```bash
./suconnect 4444
```

<details> <summary><b>Password</b></summary>  EeoULMCra2q0dSkYj561DX7s1CpBuOBt  </details> 

---

# 🔹 Level 21

### 🎯 Goal

Cronjob analysis.

### 📘 Theory

Cron runs scheduled scripts.

### 🛠 Walkthrough

Inspect:

```bash
cat /etc/cron.d/cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
cat /tmp/<generatedfile>
```

<details> <summary><b>Password</b></summary>  tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q  </details>

---

# 🔹 Level 22

### 🎯 Goal

Predict MD5 filename.

### 📘 Theory

`md5sum`

### 🛠 Walkthrough

```bash
echo I am user bandit23 | md5sum
cat /tmp/<hash>
```

<details> <summary><b>Password</b></summary>  0Zf11ioIjMVN551jX3CmStKLYqjk54Ga  </details>

---

# 🔹 Level 23

### 🎯 Goal

Exploit cron script execution.

### 📘 Theory

Writable spool directory.

### 🛠 Walkthrough

Create script:

```bash
cat /etc/bandit_pass/bandit24 > /tmp/pass
```

Copy into:

```bash
/var/spool/bandit24/foo/
```

<details> <summary><b>Password</b></summary>  gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8  </details>

---

# 🔹 Level 24

### 🎯 Goal

Bruteforce 4-digit PIN.

### 📘 Theory

Looping with `seq`.

### 🛠 Walkthrough

Generate combinations:

```bash
for pin in $(seq -w 0000 9999); do
  echo "$password $pin"
done
```

<details> <summary><b>Password</b></summary>  iCi86ttT4KSNe1armKiwbQNmB3YJP3q4  </details>

---

# 🔹 Level 25

### 🎯 Goal

Check Terminal

### 📘 Theory
```
cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh
export TERM=linux
exec more ~/text.txt
exit 0
```

<details> <summary><b>Password</b></summary>  -----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEApis2AuoooEqeYWamtwX2k5z9uU1Afl2F8VyXQqbv/LTrIwdW
pTfaeRHXzr0Y0a5Oe3GB/+W2+PReif+bPZlzTY1XFwpk+DiHk1kmL0moEW8HJuT9
/5XbnpjSzn0eEAfFax2OcopjrzVqdBJQerkj0puv3UXY07AskgkyD5XepwGAlJOG
xZsMq1oZqQ0W29aBtfykuGie2bxroRjuAPrYM4o3MMmtlNE5fC4G9Ihq0eq73MDi
1ze6d2jIGce873qxn308BA2qhRPJNEbnPev5gI+5tU+UxebW8KLbk0EhoXB953Ix
3lgOIrT9Y6skRjsMSFmC6WN/O7ovu8QzGqxdywIDAQABAoIBAAaXoETtVT9GtpHW
qLaKHgYtLEO1tOFOhInWyolyZgL4inuRRva3CIvVEWK6TcnDyIlNL4MfcerehwGi
il4fQFvLR7E6UFcopvhJiSJHIcvPQ9FfNFR3dYcNOQ/IFvE73bEqMwSISPwiel6w
e1DjF3C7jHaS1s9PJfWFN982aublL/yLbJP+ou3ifdljS7QzjWZA8NRiMwmBGPIh
Yq8weR3jIVQl3ndEYxO7Cr/wXXebZwlP6CPZb67rBy0jg+366mxQbDZIwZYEaUME
zY5izFclr/kKj4s7NTRkC76Yx+rTNP5+BX+JT+rgz5aoQq8ghMw43NYwxjXym/MX
c8X8g0ECgYEA1crBUAR1gSkM+5mGjjoFLJKrFP+IhUHFh25qGI4Dcxxh1f3M53le
wF1rkp5SJnHRFm9IW3gM1JoF0PQxI5aXHRGHphwPeKnsQ/xQBRWCeYpqTme9amJV
tD3aDHkpIhYxkNxqol5gDCAt6tdFSxqPaNfdfsfaAOXiKGrQESUjIBcCgYEAxvmI
2ROJsBXaiM4Iyg9hUpjZIn8TW2UlH76pojFG6/KBd1NcnW3fu0ZUU790wAu7QbbU
i7pieeqCqSYcZsmkhnOvbdx54A6NNCR2btc+si6pDOe1jdsGdXISDRHFb9QxjZCj
6xzWMNvb5n1yUb9w9nfN1PZzATfUsOV+Fy8CbG0CgYEAifkTLwfhqZyLk2huTSWm
pzB0ltWfDpj22MNqVzR3h3d+sHLeJVjPzIe9396rF8KGdNsWsGlWpnJMZKDjgZsz
JQBmMc6UMYRARVP1dIKANN4eY0FSHfEebHcqXLho0mXOUTXe37DWfZza5V9Oify3
JquBd8uUptW1Ue41H4t/ErsCgYEArc5FYtF1QXIlfcDz3oUGz16itUZpgzlb71nd
1cbTm8EupCwWR5I1j+IEQU+JTUQyI1nwWcnKwZI+5kBbKNJUu/mLsRyY/UXYxEZh
ibrNklm94373kV1US/0DlZUDcQba7jz9Yp/C3dT/RlwoIw5mP3UxQCizFspNKOSe
euPeaxUCgYEAntklXwBbokgdDup/u/3ms5Lb/bm22zDOCg2HrlWQCqKEkWkAO6R5
/Wwyqhp/wTl8VXjxWo+W+DmewGdPHGQQ5fFdqgpuQpGUq24YZS8m66v5ANBwd76t
IZdtF5HXs2S5CADTwniUS5mX1HO9l5gUkk+h0cH5JnPtsMCnAUM+BRY=
-----END RSA PRIVATE KEY-----  </details>

---

# 🔹 Level 26

### 🎯 Goal

`make the terminal very small.`

`more` → can open `vim`.
Press:
```
v
```
Then:
```
:set shell=/bin/bash
:shell
```

Use SUID binary.
```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

<details> <summary><b>Password</b></summary>  upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB  </details>

---

# 🔹 Level 27

### 🎯 Goal

Clone git repo.

### 📘 Theory

Git over SSH.

```bash
git clone ssh://...
cat README
```

<details> <summary><b>Password</b></summary>  Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN  </details>

---

# 🔹 Level 28

### 🎯 Goal

Check git history.

### 📘 Theory

```bash
git log
git show <commit>
```

<details> <summary><b>Password</b></summary>  4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7  </details>

---

# 🔹 Level 29

### 🎯 Goal

Switch branch.

```bash
git branch -a
git checkout dev
```

<details> <summary><b>Password</b></summary>  qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL  </details>

---

# 🔹 Level 30

### 🎯 Goal

Check git tags.

```bash
git tag
git show secret
```

<details> <summary><b>Password</b></summary>  fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy  </details>

---

# 🔹 Level 31

### 🎯 Goal

Push file despite .gitignore.

### 📘 Theory

`.gitignore` ignores *.txt

Force add:

```bash
git add -f key.txt
git push
```

<details> <summary><b>Password</b></summary>  3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K  </details>

---

# 🔹 Level 32

### 🎯 Goal

Escape restricted shell using `$0`.

### 📘 Theory

`$0` references shell.

```bash
$0
whoami
cat /etc/bandit_pass/bandit33
```

<details> <summary><b>Password</b></summary>  tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0  </details>

---

# 🔹 Level 33

Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!

---
# 🏆 Conclusion

Bandit teaches:

- Linux fundamentals
- File permissions
- SUID
- Networking
- Encoding
- Git exploitation
- Cron abuse
- Shell escaping
---

## 🧑‍💻 Author

Ghost -  Cyber-security Learner & CTF Player
