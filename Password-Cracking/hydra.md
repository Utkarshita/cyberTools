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

## Core Features
- Brute-Force Attacks: Attempts to find valid login credentials.
- Multiple Protocols: Supports SSH, FTP, HTTP, RDP, SMB, etc.
- Parallelized Attacks: Allows multiple concurrent connection attempts.
- Custom Wordlists: Use your own or prebuilt password lists.
- Proxy Support: Route through proxies for anonymity.
- Session Management: Resume or ignore saved sessions.
- Flexible Options: Choose users, passwords, ports, and more.
- Interactive Mode: Terminal-based UI for manual contro

## Data Sources Required
-Target Host Information (IP or domain)
- Protocol and Port
- Username(s) or userlists
- Password(s) or wordlists
- Proxy settings (optional)

## Basic Syntax
```bash
hydra [OPTIONS] TARGET PROTOCOL
```
### Target Specification
| Option          | Description                                                    |
| --------------- | -------------------------------------------------------------- |
| `-l <login>`    | Use a **single login name** (e.g., `admin`)                    |
| `-L <file>`     | Use a **list of usernames** from file                          |
| `-p <password>` | Use a **single password**                                      |
| `-P <file>`     | Use a **list of passwords** from file                          |
| `-C <file>`     | Use a **combo file** (format: `username:password`)             |
| `-M <file>`     | Use a **list of target IPs** from file                         |
| `-t <tasks>`    | Number of **parallel tasks** (default: 16)                     |
| `-s <port>`     | Custom **port number**                                         |
| `-S`            | Use **SSL** connection                                         |
| `-v / -V / -d`  | Verbose output (`-v`: normal, `-V`: very verbose, `-d`: debug) |
| `-f`            | Exit after first valid login found                             |
| `-o <file>`     | Save output to file                                            |
| `-u`            | Loop around users, not passwords (useful for SMTP, etc.)       |
| `-x`            | Generate passwords automatically (see below)                   |

### Advanced Options
| Option         | Description                                                           |
| -------------- | --------------------------------------------------------------------- |
| `-e nsr`       | Try **n**one, **s**ame as login, and **r**everse of login as password |
| `-R`           | Restore a previously saved session (`./hydra.restore`)                |
| `-I`           | Ignore restore file                                                   |
| `-w <timeout>` | Set timeout (in seconds)                                              |
| `-W <wait>`    | Wait time between login attempts                                      |
| `-O`           | Use old SSL (useful for legacy systems)                               |
| `-4`           | Force IPv4                                                            |
| `-6`           | Force IPv6                                                            |

### Password Generation with -x
```bash
-x min:max:charset
```
| Example     | Meaning                                                   |
| ----------- | --------------------------------------------------------- |
| `-x 4:6:a1` | Brute-force using charset `[a-z0-9]`, lengths from 4 to 6 |

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

### Hydra Module Help
```bash
hydra -U
or
man hydra
```


- Use -f to stop once a valid password is found.
-Use -o output.txt to log successful credentials.
- Use with proxychains if routing through proxy/Tor.
- Combine with nmap for service discovery before launching Hydra.


