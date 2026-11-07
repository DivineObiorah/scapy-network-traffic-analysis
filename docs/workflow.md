# Practical and GitHub Workflow

This guide follows the supplied Cisco **Lab – Packet Crafting with Scapy**. Complete the lab in your authorized Kali VM first, then document your actual results and publish the repository with Git Bash.

## 1. Prepare the lab

1. Start the Kali VM.
2. Confirm Scapy is installed:
   ```bash
   scapy --version
   ```
   If that option is not supported by your installed version, launch `scapy` and note the version shown at startup.
3. Identify the interface associated with the lab network:
   ```bash
   ip addr
   ```
   The supplied lab identifies `br-internal` as the interface with address `10.6.6.1`.
4. Confirm that `10.6.6.23` is the intended target in your isolated lab. Do not assume the address is the same in a different VM setup.

## 2. Part 1 – Investigate Scapy

Start a terminal and launch the interactive shell:

```bash
sudo su
scapy
```

At the Scapy prompt, inspect available protocols and IPv4 fields:

```python
ls()
ls(IP)
```

Record the Scapy version and your observations in `docs/lab-notes.md`.

**Screenshot checklist**
- Scapy shell showing its version.
- `ls(IP)` output showing the IPv4 fields.
- Optional: the relevant TFTP entries from `ls()`.

## 3. Part 2 – Sniff network traffic

In the Scapy shell, start a capture:

```python
sniff()
```

In a second Kali terminal, generate a small amount of authorized traffic:

```bash
ping -c 5 www.cisco.com
```

Stop the capture with `Ctrl+C`. Review the captured packets:

```python
a = _
a.summary()
```

For the internal lab network, capture on the interface identified earlier:

```python
sniff(iface="br-internal")
```

Generate traffic to the lab target from a second terminal, then stop the capture and inspect it:

```python
a = _
a.summary()
```

Capture ten ICMP packets:

```python
sniff(iface="br-internal", filter="icmp", count=10)
```

In a second terminal, ping the authorized lab target:

```bash
ping -c 10 10.6.6.23
```

When the capture completes:

```python
a = _
a.nsummary()
a[2]
```

Save the captured packets:

```python
wrpcap("capture1.pcap", a)
```

Open the PCAP in Wireshark and inspect the packet layers. Keep the capture local unless you have reviewed it and confirmed it is safe to publish.

**Screenshot checklist**
- Capture running on the correct interface.
- `nsummary()` showing the ICMP traffic.
- One packet's layer details (hide sensitive addresses if needed).
- Wireshark displaying the saved capture.

## 4. Part 3 – Create and send an ICMP packet

In one Scapy terminal, start a capture on the internal interface:

```python
sniff(iface="br-internal")
```

In a second terminal, start Scapy with the privileges required by the lab:

```bash
sudo su
scapy
```

Send the custom ICMP packet to the authorized lab target:

```python
send(IP(dst="10.6.6.23")/ICMP()/"This is a test")
```

Return to the capture terminal, stop the capture with `Ctrl+C`, and inspect it:

```python
a = _
a.nsummary()
```

Inspect the relevant request and reply packets:

```python
a[PACKET_NUMBER]
```

Replace `PACKET_NUMBER` with the actual packet index shown in your capture.

**Screenshot checklist**
- The custom ICMP send command and Scapy result.
- Capture summary showing the observed packets.
- Packet details showing the custom payload, if present.

## 5. Part 4 – Create and send a TCP SYN packet

Start a capture on the internal interface in the first Scapy terminal:

```python
sniff(iface="br-internal")
```

In the second Scapy terminal, send a SYN packet to TCP port 445 on the authorized lab target:

```python
send(IP(dst="10.6.6.23")/TCP(dport=445, flags="S"))
```

Stop the capture in the first terminal and inspect the actual returned packets:

```python
a = _
a.nsummary()
a[PACKET_NUMBER]
```

Replace `PACKET_NUMBER` with the index of the response packet. Interpret the TCP flags from your own output. A SYN-ACK (`SA`) response indicates that the target acknowledged the SYN; document only what the observed response supports.

**Screenshot checklist**
- TCP SYN send command.
- Captured response packet details showing the TCP flags.
- Your written interpretation in `docs/findings-template.md`.

## 6. Document your findings

1. Open `docs/lab-notes.md` and record the VM, Scapy version, interface, and commands you actually used.
2. Open `docs/findings-template.md` and complete each section from your own output.
3. Place screenshots in the matching `evidence/screenshots/part-*` folder.
4. Put sanitized text output in `evidence/terminal-outputs/`.
5. Review all evidence for credentials, personal data, and unrelated traffic.
6. Keep raw PCAPs out of Git unless you have checked them and intentionally decided to publish a safe copy.

## 7. Publish using Git Bash

### A. Extract and open the project folder

Extract the downloaded ZIP. In File Explorer, open the extracted `Scapy_Packet_Crafting_Lab` folder, right-click inside it, and choose **Open Git Bash here** (or navigate to it in Git Bash).

Example path (replace with your actual Windows username and extraction location):

```bash
cd "/c/Users/YOUR_WINDOWS_USERNAME/Downloads/Scapy_Packet_Crafting_Lab"
```

Check the folder:

```bash
pwd
ls -la
```

### B. Configure Git (one-time setup)

```bash
git config --global user.name "Your Name"
git config --global user.email "your-github-email@example.com"
```

Use the email associated with your GitHub account, or a GitHub-provided noreply address if you prefer not to expose your personal email.

### C. Initialize and commit

```bash
git init
git branch -M main
git status
git add .
git status
git commit -m "Add Scapy packet crafting lab"
```

Review `git status` before committing. Confirm that no credentials, private traffic captures, or unrelated files are staged.

### D. Create the GitHub repository

On GitHub:
1. Sign in and select **New repository**.
2. Repository name: `Scapy_Packet_Crafting_Lab`
3. Description: `Hands-on network reconnaissance and packet crafting lab using Python Scapy, covering traffic sniffing, custom ICMP packets, TCP SYN scanning, and packet analysis.`
4. Choose **Public** if you want it visible on your profile, or **Private** if you prefer.
5. Do not initialize it with a README, license, or `.gitignore` because those files are already in this local project.
6. Create the repository and copy its HTTPS URL.

### E. Connect and push

Replace the example URL with the HTTPS URL copied from your own GitHub repository:

```bash
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/Scapy_Packet_Crafting_Lab.git
git remote -v
git push -u origin main
```

GitHub may open a browser sign-in or ask you to authenticate. Use GitHub's supported sign-in flow or a personal access token when prompted; your GitHub password is not accepted for ordinary HTTPS Git operations.

### F. Verify

Refresh your GitHub repository page. Confirm that:
- README renders correctly.
- `docs/`, `evidence/`, `scripts/`, and `references/` are visible.
- Your screenshots are present.
- No secrets or unreviewed PCAP files were uploaded.

For later updates:

```bash
git status
git add .
git status
git commit -m "Add Scapy lab evidence and findings"
git push
```

If you intentionally want to publish a reviewed PCAP that is ignored by `.gitignore`, use `git add -f evidence/pcaps/your-sanitized-capture.pcap` only after confirming it contains no sensitive traffic.

## 8. Troubleshooting

- **`git` is not recognized:** Install Git for Windows, reopen Git Bash, and run `git --version`.
- **Nothing to commit:** Check `git status`; the starter files may already have been committed.
- **Remote already exists:** Run `git remote -v`. If it points to the wrong repository, correct it with `git remote set-url origin YOUR_REPOSITORY_URL`.
- **Authentication failed:** Complete GitHub's browser authentication or configure a supported credential manager/token.
- **Push rejected:** Check whether the remote repository was initialized with files. For this workflow, create the remote without a README/license/`.gitignore`. Do not force-push blindly.
