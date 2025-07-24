# John the Ripper
John the Ripper is a fast, versatile, and customizable password cracking tool that helps ethical hackers and penetration testers recover plaintext passwords from hash dumps. It supports a wide range of formats — from Unix/Linux hashes to Windows, documents, encrypted ZIPs, and more.

### Purpose
John the ripper is primarily used for security testing and penetration testing to identify weakness in passwords.
- It offers a range of functionaliteie including brute-force attacks, dictianary attacks, and support for multiple password formats.

## Supported Hash Formats (Examples)
| Format                                     | Use Case                      |
| ------------------------------------------ | ----------------------------- |
| `raw-md5`, `sha1`, `bcrypt`, `sha512crypt` | Linux shadow passwords        |
| `nt`, `lm`                                 | Windows hashes                |
| `zip`, `rar`, `pdf`, `office`              | Encrypted file passwords      |
| `krb5`, `mysql`, `md5crypt`                | Network services or DB hashes |
To view all supported formats:
```bash
john --list=formats
```

## Commands
| **Command**                               | **Description**                     | **Example**                                      | **Notes**                               |
| ----------------------------------------- | ----------------------------------- | ------------------------------------------------ | --------------------------------------- |
| `john [file]`                             | Basic crack with default mode       | `john hashes.txt`                                | Uses “single” mode by default           |
| `john --wordlist=[file] [hashes]`         | Dictionary attack                   | `john --wordlist=rockyou.txt hashes.txt`         | Most commonly used mode                 |
| `john --incremental [file]`               | Brute-force all character combos    | `john --incremental hashes.txt`                  | Slow but thorough                       |
| `john --incremental=digits [file]`        | Brute-force digits only             | `john --incremental=digits hashes.txt`           | Use for numeric-only PINs               |
| `john --single [file]`                    | Single crack mode (fast)            | `john --single hashes.txt`                       | Uses usernames/etc. as clues            |
| `john --external=mode [file]`             | Use custom cracking logic           | `john --external=Markov hashes.txt`              | Advanced usage                          |
| `john --format=[type] [file]`             | Specify hash format                 | `john --format=nt hashes.txt`                    | NT for Windows hashes                   |
| `john --rules --wordlist=[file] [hashes]` | Wordlist + smart mutations          | `john --rules --wordlist=rockyou.txt hashes.txt` | Very effective hybrid attack            |
| `john --show [file]`                      | Display cracked passwords           | `john --show hashes.txt`                         | Shows username\:password format         |
| `john --test`                             | Benchmark JtR speed                 | `john --test`                                    | Useful for checking performance         |
| `john --test --format=[type]`             | Benchmark for a specific format     | `john --test --format=raw-md5`                   | Compare algorithm speeds                |
| `john --session=[name] [file]`            | Save cracking session               | `john --session=run1 hashes.txt`                 | Saves session progress                  |
| `john --restore=[name]`                   | Resume session                      | `john --restore=run1`                            | Continues cracking where you left off   |
| `john --status=[name]`                    | Check status of session             | `john --status=run1`                             | Shows % done, speed                     |
| `john --pot=[file]`                       | Use custom cracked password file    | `john --pot=my.pot hashes.txt`                   | Reuse cracked results                   |
| `john --list=formats`                     | List supported hash types           | `john --list=formats`                            | Use to confirm hash support             |
| `john --list=rules`                       | List available rule sets            | `john --list=rules`                              | Great for wordlist mutation rules       |
| `john --list=inc-modes`                   | View all brute-force modes          | `john --list=inc-modes`                          | E.g., digits, alpha, all                |
| `john --list=ext-modes`                   | View all external cracking modes    | `john --list=ext-modes`                          | For `--external` use                    |
| `john --list=build-info`                  | System & build info                 | `john --list=build-info`                         | Debugging and optimization              |
| `unshadow passwd shadow > file.txt`       | Merge `/etc/passwd` + `/etc/shadow` | `unshadow /etc/passwd /etc/shadow > hashes.txt`  | Use before cracking Linux system hashes |
| `zip2john file.zip > hash.txt`            | Extract hash from ZIP               | `zip2john secret.zip > ziphash.txt`              | Then run: `john ziphash.txt`            |
| `pdf2john.pl file.pdf > hash.txt`         | Extract hash from PDF               | `pdf2john.pl file.pdf > pdfhash.txt`             | Then run: `john pdfhash.txt`            |
| `rar2john file.rar > hash.txt`            | Extract hash from RAR               | `rar2john secret.rar > rarhash.txt`              | Then run: `john rarhash.txt`            |

## Key Options & Flags
| Option            | Use                                            |
| ----------------- | ---------------------------------------------- |
| `--wordlist=FILE` | Specify wordlist file (like `rockyou.txt`)     |
| `--rules`         | Enable password mutation (hybrid)              |
| `--format=TYPE`   | Force specific hash format (e.g., NT, raw-md5) |
| `--session=NAME`  | Save cracking session                          |
| `--restore=NAME`  | Resume session later                           |
| `--pot=FILE`      | Use specific potfile for cracked passwords     |
| `--show`          | Display cracked passwords                      |
| `--test`          | Benchmark speed for current system             |

### Practical Examples
1. Crack NTLM Hash with Wordlist:
```bash
john --format=nt --wordlist=rockyou.txt hashes.txt
```
2. Brute-force Linux Shadow File:
```bash
john --incremental=all shadow_hashes.txt
```
3. Save and Restore a Cracking Session:
```bash
john --session=myrun --wordlist=rockyou.txt hashes.txt
john --restore=myrun
```
4. See What You’ve Cracked:
```bash
john --show hashes.txt
```
5. Test JtR on Your Machine:
```bash
john --test
john --test --format=raw-md5
```



