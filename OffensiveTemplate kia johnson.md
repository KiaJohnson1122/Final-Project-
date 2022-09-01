# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
|Port  | Services
|-----------------|
|22    | SSH
| 80   | HTTP
|111   | RPCbin
| 139  | netbios-ssn
| 445  | Microsoft-DS

Nmap scan results for each machine reveal the below services and OS details:

```bash
$ nmap -Pn -sV -p 80,111,139,445 192.168.1.110

```

This scan identifies the services below as potential points of entry:
- Target 1
  - List of
  - Exposed Services

_TODO: Fill out the list below. Include severity, and CVE numbers, if possible._

The following vulnerabilities were identified on each target:
CvE ( common vunerability and exposure)
| severity |Base Score |
|----------|-----------|
| None     | 0         |
| Low      |   0.1-3.9 |
| Medium   | 4.0-6.9   |
| High     | 7.0-8.9   |
| Critical | 9.0-10.0  |

|CVE ID       |Score       | Vulnerability Description
|-------------|-----------|---------------------------|
|CVE-2001-0572|7.5        | DUe to weak passwords for their users, easy access by SSH
|CVE-2021-24585| 6.5      | outputting hashed password, usernames and email address being used
wpscan
|CVE-2002-1374 | 7.5      | Brute force common password MySQL access to data base 
|CVE-2019-5629 | 7.8      | Using python to get privileges to gain system privileges

_TODO: Include vulnerability scan results to prove the identified vulnerabilities._

### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: _TODO: Insert `flag1.txt` hash value_
    - Used grep to find location of flag
    logged into Micael account with the password (Michael)
    -used wpscan to find the username 


      - _TODO: Identify the exploit used_
      - _TODO: grep 
  - `flag2.txt`: _TODO: Insert `flag2.txt` hash value_
    - **Exploit Used**
      - we used the find command in order to find it 
      - _TODO: cd /var/www
      cat flag2.txt 


      **Exploit Used**

      Flag 3 
       we figured out the password by gaining access to hash password from michael wordpress config file Password R@v3nSecurity
       gained access to MySQL - found password hash for Michael and Steven


       - Used John the ripper to break into hash of passwords to gain access to Steven 
       - john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
       Using wordlist and hash.txt file we got Steven password 
       pink84

       Flag 4 
       using sudo -l seen it was access to python
       using a spawn script 

       Sudo python -c "import pty:pty.spawn("/bin/bash")'
       gained access to root and bash 
       this command helped us find flag 4 

       *Screenshots in folder labled Flag 1-4
       * Screenshots in folder supports findings as well 