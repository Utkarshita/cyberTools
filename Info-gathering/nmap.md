# Nmap 


## Overview:
Nmap (short for Network Mapper) is an open-source tool used for network discovery and security auditing. It's one of the most widely used tools to map networks, discover live hosts, detect open ports, and identify running services or operating systems.

## Use Cases:
- Discovering live hosts on a network
- Identifying open/filtered/closed ports
- OS and version detection
- Vulnerability scanning using NSE (Nmap Scripting Engine)
- Firewall evasion and spoofing

## Real-World Use:
- Reconnaissance before exploitation
- Identifying vulnerable services and versions
- Mapping internal networks during Red Team assessments
- Finding open ports and misconfigurations
  
## Basic Scanning Techniques:

### Scan IP address (Targets)

| **Command**                                 | **Description**                                                   |
|---------------------------------------------|-------------------------------------------------------------------|
| `nmap 192.168.1.4`                              | Scan a single host IP                                             |
| `nmap 192.168.1.0/24`                       | Scan a Class C **subnet range**                                   |
| `nmap 192.168.1.4-100`                          | Scan the range of IPs between 10.1.1.5 up to 10.1.1.100            |
| `nmap -iL hosts.txt`                         | Scan the IP addresses listed in text file `"hosts.txt"`           |
| `nmap 192.168.1.3 192.168.1.4 192.168.1.5`            | Scan the 3 specified IPs only                                     |
| `nmap www.somedomain.com`                   | First resolve the IP of the domain and then scan its IP address   |

### Port Related Commands

| **Command**                                 | **Description**                                        |
|---------------------------------------------|--------------------------------------------------------|
| `nmap -p80 192.168.1.4`                         | Scan only port 80 for specified host                   |
| `nmap -p20-23 192.168.1.4`                      | Scan ports 20 up to 23 for specified host              |
| `nmap -p80,88,8000 192.168.1.4`                 | Scan ports 80, 88, and 8000 only                       |
| `nmap -p- 192.168.1.4`                          | Scan **all** ports for specified host                  |
| `nmap -sS -sU -p U:53,T:22 192.168.1.4`         | Scan ports **UDP 53** and **TCP 22**                   |
| `nmap -p http,ssh 192.168.1.4`                  | Scan **http** and **ssh** ports for specified host     |

### Different Scan Types

| **Command**                 | **Description**                      |
|-----------------------------|--------------------------------------|
| `nmap -sS 192.168.1.4`         | TCP SYN Scan (best option)           |
| `nmap -sT 192.168.1.4`         | Full TCP connect scan                |
| `nmap -sU 192.168.1.4`         | Scan UDP ports                       |
| `nmap -sP 192.168.1.0/24`      | Do a Ping scan only                  |
| `nmap -Pn 192.168.1.4`         | Don't ping the host, assume it's up  |

### Identify Versions of Services and Operating Systems

| Command              | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `nmap -sV 192.168.1.4`  | Version detection scan of open ports (services)                             |
| `nmap -O 192.168.1.4`   | Identify Operating System version                                            |
| `nmap -A 192.168.1.4`   | Combines OS detection, version detection, script scanning, and traceroute    |

### Scan Timings

| Command              | Description                                                                       |
|----------------------|-----------------------------------------------------------------------------------|
| `nmap -T0 192.168.1.4`  | Slowest scan (to avoid IDS)                                                       |
| `nmap -T1 192.168.1.4`  | Sneaky (to avoid IDS)                                                             |
| `nmap -T2 192.168.1.4`  | Polite (10 times slower than T3)                                                  |
| `nmap -T3 192.168.1.4`  | Default scan timing (normal)                                                      |
| `nmap -T4 192.168.1.4`  | Aggressive (fast and fairly accurate)                                             |
| `nmap -T5 192.168.1.4`  | Very Aggressive (might miss open ports, very likely to be detected by firewalls)  |

### Output types

| Command                             | Description                                       |
| ----------------------------------- | ------------------------------------------------- |
| `nmap -oN scan.txt 192.168.1.0/24`  | Normal text format                                |
| `nmap -oG scan.grep 192.168.1.0/24` | Grepable format (useful for searching in file)    |
| `nmap -oX scan.xml 192.168.1.0/24`  | XML format                                        |
| `nmap -oA scan 192.168.1.0/24`      | Outputs in all 3 formats above with prefix `scan` |

### Discover Live Hosts

| Command                        | Description                                                     |
| ------------------------------ | --------------------------------------------------------------- |
| `nmap -PS22-25,80 192.168.1.0/24` | Discover hosts by sending TCP SYN packets to ports 22–25 and 80 |
| `nmap -Pn 192.168.1.0/24`         | Disable host discovery. Treat all hosts as online (no ping)     |
| `nmap -PE 192.168.1.0/24`         | Send ICMP Echo requests (similar to traditional ping)           |
| `nmap -sn 192.168.1.0/24`         | Ping scan (host discovery only, no port scan)                   |

### NSE Scripts

| Command                                                                   | Description                                   |
| ------------------------------------------------------------------------- | --------------------------------------------- |
| `nmap --script="name of script" 192.168.1.0/24`                              | Run the specified script towards the targets. |
| `nmap --script="name of script" --script-args="argument=arg" 192.168.1.0/24` | Run the script with the specified arguments.  |
| `nmap --script-updatedb`                                                  | Update script database                        |

### Other Useful Commands

| Command                            | Description                                |
| ---------------------------------- | ------------------------------------------ |
| `nmap -6 [IP hosts]`               | Scan IPv6 hosts                            |
| `nmap --proxies url1,url2`         | Run the scan through proxies               |
| `nmap --open`                      | Only show open ports                       |
| `nmap --script-help="script name"` | Get info and help for the specified script |
| `nmap -V`                          | Show currently installed version           |
| `nmap -S [IP address]`             | Spoof source IP                            |
| `nmap --max-parallelism [number]`  | Maximum parallel probes/connections        |
| `nmap --max-rate [number]`         | Maximum packets per second                 |



