# Penetration Testing Report: Footprinting & Network Scanning

![Cybersecurity](https://img.shields.io/badge/Cybersecurity-Pentesting-0E7C86)
![Phase](https://img.shields.io/badge/Phases-1%20%26%202-14213D)
![Program](https://img.shields.io/badge/Networkwalks-Week%2002-0E7C86)

**W2-PM-FINAL | Cybersecurity | Networkwalks**
Week 2 of the Cybersecurity & Ethical Hacking internship at Networkwalks.

📄 **Full report:** [PDF](report/W2-PM-FINAL_Penetration_Testing_Report.pdf) · [Word (.docx)](W2-PM-FINAL_Penetration_Testing_Report.docx)

---

## ⚠️ Liability Disclaimer

I performed these activities only on systems and devices where I had secured written permission or devices/systems that I own myself. All materials are for education and research purposes only. Do not use anything here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

---

## 📋 Project Details

| | |
|---|---|
| **Pentester** | Romans Angel |
| **Program / Batch** | B084-Networkwalks |
| **Date** | 12 November 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools), W2-PM5 (Zenmap Scanning) |
| **Client / Target** | 1. Networkwalks (secured written permission already) <br> 2. My own local LAN network |
| **Permission secured?** | Yes |
| **Phases covered** | **Phase 1:** Reconnaissance & Footprinting <br> **Phase 2:** Scanning & Network Discovery <br> **Phase 3-5:** In progress |

## 🎯 Introduction

This project covers footprinting the `networkwalks.com` domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5). Together they show how an attacker moves from gathering public information to mapping live hosts on a network.

Footprinting was done in Kali Linux; scanning was done on a Windows PC with Zenmap installed.

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux & Windows | Operating systems used for reconnaissance activities |
| `whois` | Find domain registration details (owner, dates, name servers) |
| `whatweb` | Fingerprint web technologies (server, CMS, plugins, IP) |
| `nslookup` | Resolve the domain name to its IP address using DNS |
| `curl -I` | Read the HTTP response headers of the website |
| `wafw00f` | Detect whether a Web Application Firewall protects the site |
| `dnsrecon` | Enumerate DNS records (NS, MX, SPF, TXT, SRV) |
| Zenmap (Nmap GUI) | Scan the local subnet to find live hosts, IPs and MAC addresses |
| Windows CMD | Local IP and MAC address identification |

## 🔍 Activities Performed

### 4.1 Footprinting & Reconnaissance (`networkwalks.com`)

| Tool | What it revealed |
|---|---|
| **WHOIS** | Public domain registration information and the domain's name servers |
| **WhatWeb** | **WordPress 7.1.4** and **WP Download Manager 3.3.76**, plus other exposed information |
| **Nslookup** | Domain resolves to **192.232.216.135** |
| **Curl `-I`** | HTTP response headers and the exposed WordPress REST API endpoint `/wp-json/` |
| **Wafw00f** | Web Application Firewall identified as **ModSecurity (SpiderLabs)** |
| **DNSRecon** | Name servers, mail servers, SPF/TXT records, service records and DNS software information |

### 4.2 Network Scanning with Zenmap (local network)

1. Used the Windows `ipconfig` command to identify the local IP address and LAN subnet.
2. Entered the subnet into Zenmap and ran a **Ping Scan** to find active hosts.
3. Identified two live hosts: `172.20.10.1` and `172.20.10.2`, along with two MAC addresses.
4. Opened the **Topology** tab, enabled the legend and saved the topology as a PDF.

## 🚨 Risk Analysis / Impact

| # | Risk / Finding | Evidence | Potential Impact | Level |
|---|---|---|---|---|
| 1 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager | Exposed version information can help identify software needing further review | 🟡 Medium |
| 2 | Server IP address identifiable | Nslookup resolved the domain to `192.232.216.135` | Reveals the network location of the web service | 🟢 Low |
| 3 | HTTP technical information exposed | Curl returned headers and exposed `/wp-json/` | May assist fingerprinting and further enumeration | 🟢 Low |
| 4 | WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Reveals information about the security architecture | 🟢 Low |
| 5 | DNS infrastructure information exposed | DNSRecon identified DNS, mail and service records | Helps build a broader infrastructure profile | 🟡 Medium |
| 6 | Multiple live hosts visible on local network | Zenmap identified two live hosts | Unknown or unauthorized devices may be present on a network | 🟡 Medium |

> **Note:** These are observations, not confirmed vulnerabilities. Only information gathering and host discovery were performed. No exploitation or vulnerability validation took place. Further authorized testing would be required to confirm any actual vulnerability.

## ✅ Recommendations

1. **Review publicly exposed technology information:** regularly review what is visible about web technologies, CMS and plugins.
2. **Keep software updated:** update CMS platforms and plugins and review them against current security advisories.
3. **Review HTTP headers:** make sure unnecessary technical information is not exposed.
4. **Review DNS records regularly:** only required information and services should be public.
5. **Properly configure and monitor the WAF:** keep ModSecurity enabled and tuned.
6. **Perform regular internal network discovery:** periodically scan your own networks for active devices.
7. **Investigate unknown devices:** verify any unexpected device found during scanning.
8. **Maintain network documentation:** keep topology and device information up to date.
9. **Perform security testing with authorization:** only test systems where authorization has been given.

## 🧠 Conclusion

Week 2 covered footprinting, reconnaissance and network scanning. Six Kali Linux tools were used to collect information about the target domain, and Zenmap was used to discover live hosts, collect IP/MAC details and build a network topology. Key takeaways: information gathering is an important part of cybersecurity, findings must be documented clearly (what was done, found, what it means, the risk and how to reduce it), and all reconnaissance and scanning must stay within an authorized scope.

## 🖼️ Evidence

| | |
|---|---|
| **1. WHOIS** | ![WHOIS](evidence/01-whois.png) |
| **2. WhatWeb** | ![WhatWeb](evidence/02-whatweb.png) |
| **3. Nslookup** | ![Nslookup](evidence/03-nslookup.png) |
| **4. Curl -I** | ![Curl](evidence/04-curl.png) |
| **5. Wafw00f** | ![Wafw00f](evidence/05-wafw00f.png) |
| **6. Zenmap ping scan** | ![Zenmap ping scan](evidence/06-zenmap-ping-scan.png) |
| **7. Zenmap topology** | ![Zenmap topology](evidence/07-zenmap-topology.png) |

## 📁 Repository Structure

```
├── README.md
├── LICENSE
├── .gitignore
├── report/
│   ├── W2-PM-FINAL_Penetration_Testing_Report.pdf
│   └── W2-PM-FINAL_Penetration_Testing_Report.docx
└── evidence/
    ├── 01-whois.png ... 07-zenmap-topology.png
```

## 👤 Author

**Romans Angel**: Cybersecurity Professional B084
LinkedIn: <https://www.linkedin.com/in/waqaskarim/>

**Program:** Cybersecurity program at Networkwalks | **Week:** 02 | **Repository:** GitHub

## 📜 License

Released under the [MIT License](LICENSE). For education and research purposes only.
