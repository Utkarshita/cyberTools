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

## Common Hydra Commands
