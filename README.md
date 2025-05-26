# 🔍 Local Network Port Scanning with Nmap

## 📘 Overview

Task - 1 of `Elevate Labs`

This project demonstrates how to scan your local network for open ports using **Nmap**, a powerful network discovery and security auditing tool. Understanding which ports are open on devices in your network is crucial for assessing potential security vulnerabilities.

---

## 🎯 Objective
- Discover active devices on your local network.
- Identify open TCP ports and associated services.
- Understand common vulnerabilities associated with exposed ports.
- Save and analyze scan results for further research.

---

## 🛠️ Tools Used

| Tool       | Description                                      | Link                                 |
|------------|--------------------------------------------------|--------------------------------------|
| Nmap       | Network scanner for open ports and services      | [nmap.org](https://nmap.org/)        |
| Wireshark* | Packet analyzer for detailed traffic inspection  | [wireshark.org](https://www.wireshark.org/) |

\*Optional but recommended for packet-level analysis.

---

## 🧭 Steps

### 1. Determine Your Local Network Range
Open a terminal or command prompt and run:
- **Windows**: `ipconfig`
- **Linux/macOS**: `ip a` or `ifconfig`

Find your local IP (e.g., `192.168.1.5`) and derive the subnet range (e.g., `192.168.1.0/24`).

### 2. Run the Scan
Perform a TCP SYN scan across your subnet:
```bash
nmap -sS 192.168.1.0/24
````

Optional: Speed up with `-T4` or include service/OS detection with `-A`.

### 3. Save Results

```bash
# Save as plain text
nmap -sS 192.168.1.0/24 -oN scan_results.txt

# Save as XML + convert to HTML
nmap -sS -oX scan.xml 192.168.1.0/24
xsltproc scan.xml -o scan.html
```

### 4. Analyze with Wireshark (Optional)

Open Wireshark → Start capture → Run scan → Use filters like:

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

![Screenshot 2025-05-26 134613](https://github.com/user-attachments/assets/8c3b4d80-8550-4c1c-b1a1-f04ec43ba635)


---

## 🔎 Example Output

```
Nmap scan report for 192.168.1.10
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
```
---

## ⚠️ Common Ports & Risks

| Port | Service | Risk                                   |
| ---- | ------- | -------------------------------------- |
| 22   | SSH     | Brute-force access if weak credentials |
| 23   | Telnet  | Insecure, unencrypted                  |
| 80   | HTTP    | Exposed web interface                  |
| 443  | HTTPS   | Misconfigured SSL can be a threat      |
| 3389 | RDP     | Remote desktop attacks                 |

---

## 🧠 Recommendations

* Disable unnecessary services.
* Use firewalls to block unneeded ports.
* Regularly scan your network for changes.
