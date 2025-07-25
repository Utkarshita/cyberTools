# Shodan

Shodan is like Google for hackers - it indexes devices instead of websites.
- Shodan is passive recon but extremely powerful — like OSINT for devices.
- It’s helped identify exposed ICS, traffic cams, even nuclear plant interfaces.
- When combined with Censys or ZoomEye, it can form a full-picture internet scan framework.

## What Shodan Finds
Shodan scans the entire internet for:
- Open ports and services (e.g., HTTP, FTP, SSH, Telnet)
- Industrial Control Systems (ICS), webcams, routers, IoT devices
- Unsecured databases (MongoDB, Elasticsearch, etc.)
- Default login pages and outdated software
- SSL certificate info
- Metadata (hostnames, banners, IP, country, etc.)

Shodan is used by red teams, researchers, pentesters, bug bounty hunters, and even nation-state actors.

## Getting Started with Shodan CLI
Install Shodan CLI
```bash
pip install shadon
```
Get Your API Key
Register at: https://account.shodan.io/register
Copy your API key from your dashboard

Initialize CLI with API Key
```bash
shodan init <your_api_key>
```

## Core Shodan CLI Syntax
```bash
shodan <command> [options]
```

## Commands
| Command  | Description | Example    | What It Does  |
| -------------- | -------------------- | -------------------------- | ---------------------- |
| `shodan search <query>`| Perform a Shodan search                     | `shodan search apache`                                  | Finds all hosts with Apache service                     |
| `shodan host <IP>` | Get detailed info about a target IP  | `shodan host 8.8.8.8`                                   | Shows open ports, org, OS, services, hostnames          |
| `shodan count <query>` | Count number of results for a search        | `shodan count nginx`                                    | Just get how many results your query returns            |
| `shodan download <filename> <query>` | Save search results to file  | `shodan download exposed_iot webcam`  | Useful for analysis, especially with lots of results    |
| `shodan parse <file>`| Extract specific fields from result file    | `shodan parse --fields ip_str,port exposed_iot.json.gz` | Filters and formats output for further processing       |
| `shodan scan submit <IP>`| Submit a new scan (Paid only)               | `shodan scan submit 1.1.1.1` | Tells Shodan to actively scan an IP                     |
| `shodan myip`| Shows your public IP address| `shodan myip`   | Basic check — useful if running from different networks |
| `shodan alert create <name> <IP>`    | Creates an alert for changes on a target IP | `shodan alert create NDA-server 192.168.1.10`      | Great for tracking asset exposure over time             |
| `shodan alert list`| Lists all your active alerts  | `shodan alert list`  | Manage and monitor your tracked assets  |
| `shodan alert delete <ID>`  | Delete alert  | `shodan alert delete 56a...ef`   | Clean up alert system    |
| `shodan alert add <alert_id> <ip>`   | Add IPs to an existing alert   | `shodan alert add 123xyz 10.0.0.5`     | Expand alert coverage          |


## Search Filters (Web & CLI)
Shodan lets you filter results with powerful search modifiers:
| **Filter**      | **Use**               | **Example**                |
| --------------- | --------------------- | -------------------------- |
| `country:`      | Search by country     | `ssh country:"IN"`         |
| `port:`         | Specific port         | `port:21 ftp`              |
| `org:`          | By organization/ISP   | `org:"BSNL"`               |
| `hostname:`     | Domain name search    | `hostname:gov.in`          |
| `os:`           | Operating system      | `os:"Windows XP"`          |
| `city:`         | City-level targeting  | `apache city:"Delhi"`      |
| `product:`      | Service/Product name  | `product:"MongoDB"`        |
| `before/after:` | Date-based search     | `nginx after:"2024-01-01"` |
| `title:`        | Search in HTTP titles | `title:"Login"`            |
| `ssl:`          | SSL Cert info search  | `ssl:"Let's Encrypt"`      |
Example: Search for unsecured MongoDB servers in India:
```bash
shodan search 'product:MongoDB port:27017 country:IN'
```

## Example Use Cases
1. Find Vulnerable Webcams
```bash
shodan search 'webcamXP'
```
Results often include admin interfaces of public IP cams.
2. Discover Exposed Elasticsearch Servers
```bash
shodan search 'port:9200 product:ElasticSearch'
```
Can reveal live data dumps and unsecured logs.
3. Check What a Target IP is Running
```bash
shodan host 104.244.42.1
```
Gets full data: open ports, SSL info, geo-location, org, technologies.
4. Track Unsecured Login Pages
```bash
shodan search 'http.title:"Login" country:IN'
```
Finds admin panels, exposed control panels, etc.



