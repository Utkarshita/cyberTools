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
| **Command**          | **Description**                     | **Example**                                          |
| -------------------- | ----------------------------------- | ---------------------------------------------------- |
| `shodan search`      | Search for devices or services      | `shodan search apache`                               |
| `shodan host`        | Get all info about an IP            | `shodan host 8.8.8.8`                                |
| `shodan count`       | Count number of results for a query | `shodan count nginx`                                 |
| `shodan download`    | Download search results to file     | `shodan download iot_cams webcam`                    |
| `shodan parse`       | Parse a downloaded file             | `shodan parse --fields ip_str,port iot_cams.json.gz` |
| `shodan scan submit` | Submit an IP/host to scan           | `shodan scan submit 1.1.1.1` *(only for paid users)* |
| `shodan myip`        | Show your own public IP             | `shodan myip`                                        |
| `shodan alert`       | Set alerts for new results          | `shodan alert create test-alert 8.8.8.8`             |
| `shodan info`        | Your API key usage & limits         | `shodan info`                                        |

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
2. Discover Exposed Elasticsearch Servers
```bash
shodan search 'port:9200 product:ElasticSearch'
```
3. Check What a Target IP is Running
```bash
shodan host 104.244.42.1
```
4. Track Unsecured Login Pages
```bash
shodan search 'http.title:"Login" country:IN'
```


