# Wireshark
Network Packet Analyzer

## What It Does
- Capture live network packets from an interface
- Inspect and analyze each packet layer-by-layer (Ethernet, IP, TCP, etc.)
- Filter specific protocols like HTTP, DNS, FTP, ARP, etc.
- Reconstruct sessions (e.g., see entire HTTP requests/responses)
- Troubleshoot slow networks or find abnormal behavior
- Perform deep packet inspection (DPI) — useful in hacking, forensics, and debugging

## Interface Overview
- Capture Panel: Start/pause recording from specific interfaces (Wi-Fi, Ethernet, etc.)
- Packet List: Each row is a captured packet
- Packet Details: Layer-by-layer breakdown of a packet (Frame, IP, TCP, etc.)
- Packet Bytes: Hex view
- Filter Bar: Apply display filters (e.g., http, ip.addr == 192.168.1.1)

## Capture Filters vs Display Filters
| Type               | Use              | Example                        |
| ------------------ | ---------------- | ------------------------------ |
| **Capture Filter** | Before capturing | `port 80`                      |
| **Display Filter** | After capturing  | `http.request.method == "GET"` |
Capture Filters are used to limit what gets saved.
Display Filters let you drill down into specific packets post-capture.

## Display Filters
| Filter                        | Description                                |
| ----------------------------- | ------------------------------------------ |
| `ip.addr == 192.168.1.5`      | Show all packets to/from this IP           |
| `tcp.port == 443`             | Show packets using port 443                |
| `http`                        | Show only HTTP traffic                     |
| `dns`                         | Show only DNS packets                      |
| `arp`                         | ARP protocol packets                       |
| `icmp`                        | Ping/echo traffic                          |
| `tcp.flags.syn == 1`          | Show TCP SYN packets (start of connection) |
| `tcp.analysis.retransmission` | Find TCP retransmissions (slow networks)   |
| `frame contains "password"`   | Find text that contains “password”         |
combined filters:
```bash
ip.src == 192.168.1.2 && tcp.dstport == 80
```
## TShark – Terminal Version of Wireshark
Wireshark GUI is great for visualization. But in automation/scripts or headless servers, we use TShark.
### Basic Commands
| Command                           | Description                    |
| --------------------------------- | ------------------------------ |
| `tshark -D`                       | List available interfaces      |
| `tshark -i eth0`                  | Start capture on eth0          |
| `tshark -i wlan0 -c 100`          | Capture 100 packets from wlan0 |
| `tshark -i eth0 -w output.pcap`   | Save packets to file           |
| `tshark -r output.pcap`           | Read from saved file           |
| `tshark -r output.pcap -Y "http"` | Filter HTTP from capture       |
| `tshark -i wlan0 -f "port 80"`    | Capture filter for port 80     |

## Example Use Cases
1. Analyze a DNS Attack
```bash
dns.qry.name == "malicious-domain.com"
```
2. Reconstruct HTTP GET Requests
```bash
http.request.method == "GET"
```
3. Detect ARP Spoofing
```bash
arp.duplicate-address-detected == 1
```
4. Find Login Credentials in Plaintext Protocols
```bash
ftp || telnet || http && frame contains "login"
```
Many insecure services send username/password in plaintext, which Wireshark can easily sniff if not encrypted.

## Smart Features in GUI
| Feature                             | Use                                         |
| ----------------------------------- | ------------------------------------------- |
| **Follow TCP Stream**               | Reconstruct chat/login/session              |
| **Color Rules**                     | Quickly highlight traffic types             |
| **Statistics > Protocol Hierarchy** | Protocol breakdown                          |
| **Statistics > Conversations**      | See IP ↔ IP interaction                     |
| **Export Objects > HTTP**           | Download files/images transmitted over HTTP |



