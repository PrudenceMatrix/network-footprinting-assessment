# 🔐 Networkwalks — Footprinting & Reconnaissance

> **Cybersecurity Practical Portfolio | Passive Reconnaissance & OSINT**

![Cybersecurity](https://img.shields.io/badge/Focus-Cybersecurity-red)
![Reconnaissance](https://img.shields.io/badge/Phase-Reconnaissance-blue)
![Kali Linux](https://img.shields.io/badge/Platform-Kali%20Linux-purple)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 📌 Project Overview

This repository documents a practical **footprinting and reconnaissance exercise** performed against the authorized target domain:

**`networkwalks.com`**

The objective was to understand how publicly accessible information can be collected during the reconnaissance phase of a cybersecurity assessment.

The assessment focused on:

* Domain registration information
* DNS infrastructure
* Web technology fingerprinting
* IP address identification
* HTTP response headers
* Web Application Firewall identification
* Public-source OSINT
* Subdomain discovery
* Reconnaissance limitations and observations

All activities documented in this repository were performed within the authorized educational scope of the exercise.

---

## ⚠️ Authorization & Responsible Use

This project is intended for **authorized cybersecurity education and research**.

The techniques documented here should only be used against systems where the tester has permission to perform security testing.

No exploitation or destructive activity is documented as part of this reconnaissance exercise.

> **Important:** Reconnaissance information does not automatically represent a confirmed vulnerability. Findings should be validated through authorized security testing before being classified as vulnerabilities.

---

# 🎯 Objectives

The main objectives of this practical were to:

1. Perform domain reconnaissance.
2. Identify publicly available registration information.
3. Resolve the target domain to its IP address.
4. Identify web technologies used by the target.
5. Inspect HTTP response headers.
6. Identify the Web Application Firewall.
7. Enumerate publicly visible DNS records.
8. Use OSINT sources to search for additional domain information.
9. Document findings professionally.
10. Understand how reconnaissance contributes to the early stages of a penetration test.

---

# 🛠️ Tools Used

| Tool             | Purpose                                               | Evidence                                                   |
| ---------------- | ----------------------------------------------------- | ---------------------------------------------------------- |
| **WHOIS**        | Domain registration and ownership-related information | [View WHOIS Evidence](evidence/whois.jpg)                  |
| **WhatWeb**      | Web technology fingerprinting                         | [View WhatWeb Evidence](evidence/whatweb.jpg)              |
| **Nslookup**     | DNS resolution and IP identification                  | [View Nslookup Evidence](evidence/nslookup.jpg)            |
| **Curl**         | HTTP response-header inspection                       | [View Curl Evidence](evidence/curl.jpg)                    |
| **Wafw00f**      | Web Application Firewall identification               | [View Wafw00f Evidence](evidence/wafw00f.jpg)              |
| **DNSRecon**     | DNS record enumeration                                | [View DNSRecon Evidence](evidence/dnsrecon.jpg)            |
| **theHarvester** | OSINT and public-source reconnaissance                | [View Baidu Evidence](evidence/theharvester-baidu.jpg)     |
| **theHarvester** | Multi-source reconnaissance                           | [View All-Sources Evidence](evidence/theharvester-all.jpg) |

---

# 🖥️ Environment

### Operating System

**Kali Linux**

### Target

```text
networkwalks.com
```

### Reconnaissance Phase

```text
Phase 1 — Reconnaissance & Footprinting
```

---

# 1. 🔎 WHOIS

## Objective

WHOIS was used to obtain publicly available domain-registration information.

## Command

```bash
whois networkwalks.com
```

## Key Results

The WHOIS output identified:

* Domain: `networkwalks.com`
* Registrar: **GoDaddy.com, LLC**
* Creation date: **2019-11-06**
* Registry expiration: **2027-11-06**
* DNSSEC: **unsigned**
* Name servers including:

  * `NS6135.HOSTGATOR.COM`
  * `NS6136.HOSTGATOR.COM`

The registration information also showed privacy protection through **Domains By Proxy, LLC**.

## Security Relevance

WHOIS information can help establish an initial profile of a target's domain infrastructure.

Registration dates, registrar information, domain status and name servers can all contribute to reconnaissance.

## Evidence

📸 **WHOIS Screenshot**

[Open `whois.jpg`](evidence/whois.jpg)

---

# 2. 🌐 WhatWeb

## Objective

WhatWeb was used to identify technologies and services exposed by the target website.

## Command

```bash
whatweb networkwalks.com
```

## Key Results

The scan identified:

* Apache
* WordPress
* WordPress Download Manager
* Bootstrap
* jQuery 3.7.1
* Google Tag Manager
* HTML5
* Open Graph Protocol
* IP address: `192.232.216.135`
* Website title: **Networkwalks Academy**

The output identified:

```text
WordPress 7.1
WordPress Download Manager 3.3.58
```

## Security Relevance

Technology fingerprinting allows a security professional to understand the externally visible technology stack.

Known technologies and versions can then be compared against security advisories during an authorized assessment.

> Identification of a technology or version is **not proof of a vulnerability**.

## Evidence

📸 **WhatWeb Screenshot**

[Open `whatweb.jpg`](evidence/whatweb.jpg)

---

# 3. 🌍 Nslookup

## Objective

Nslookup was used to resolve the target domain to an IP address.

## Command

```bash
nslookup networkwalks.com
```

## Key Result

The DNS query returned:

```text
Name:    networkwalks.com
Address: 192.232.216.135
```

The DNS server used during the query was:

```text
8.8.8.8
```

## Security Relevance

DNS resolution provides an important connection between a domain name and its publicly reachable infrastructure.

The discovered IP address can be used as an input for further **authorized** assessment.

## Evidence

📸 **Nslookup Screenshot**

[Open `nslookup.jpg`](evidence/nslookup.jpg)

---

# 4. 📡 Curl

## Objective

Curl was used to inspect the HTTP response headers returned by the website.

## Command

```bash
curl -I https://networkwalks.com
```

## Key Results

The server returned:

```text
HTTP/2 200
```

The response exposed information including:

```text
server: Apache
content-type: text/html
```

The response also exposed WordPress-related API references including:

```text
/wp-json/
```

## Security Relevance

HTTP response headers can reveal information about the web server and application.

This information may assist technology fingerprinting and subsequent authorized reconnaissance.

## Evidence

📸 **Curl Screenshot**

[Open `curl.jpg`](evidence/curl.jpg)

---

# 5. 🛡️ Wafw00f

## Objective

Wafw00f was used to determine whether the target website was protected by a Web Application Firewall.

## Command

```bash
wafw00f networkwalks.com
```

## Key Result

The tool identified:

```text
ModSecurity (SpiderLabs)
```

as the Web Application Firewall protecting the website.

## Security Relevance

A WAF provides an additional defensive layer between external requests and a web application.

Knowing that a WAF exists is useful during an authorized security assessment because it helps explain the target's defensive architecture.

## Evidence

📸 **Wafw00f Screenshot**

[Open `wafw00f.jpg`](evidence/wafw00f.jpg)

---

# 6. 🗂️ DNSRecon

## Objective

DNSRecon was used to enumerate publicly accessible DNS records.

## Command

```bash
dnsrecon -d networkwalks.com
```

## Key Results

The scan identified:

### SOA

```text
ns6135.hostgator.com
50.87.144.87
```

### Name Servers

```text
ns6135.hostgator.com
ns6136.hostgator.com
```

### A Record

```text
networkwalks.com
192.232.216.135
```

### MX Record

```text
mail.networkwalks.com
192.232.216.135
```

### TXT Records

The output included a Google site-verification record and an SPF record.

The SPF record included:

```text
v=spf1 +a +mx +ip4:50.87.144.87 +include:websitewelcome.com ~all
```

### SRV Records

The scan also identified `_autodiscover._tcp` service records associated with cPanel email discovery.

## Security Relevance

DNS enumeration can reveal information about:

* Name servers
* Mail infrastructure
* IP addresses
* Email services
* SPF configuration
* Service discovery records

This information can contribute to an external infrastructure map.

## Evidence

📸 **DNSRecon Screenshot**

[Open `dnsrecon.jpg`](evidence/dnsrecon.jpg)

---

# 7. 🕵️ theHarvester — Baidu

## Objective

TheHarvester was used to search public sources for domain-related information.

## Command

```bash
theHarvester -d networkwalks.com -l 1000 -b baidu
```

## Result

The tool reported:

```text
No IPs found.
No emails found.
No people found.
No hosts found.
```

## Security Relevance

An empty result from a particular search provider does not prove that information does not exist.

It simply means that the selected source did not return useful results during this execution.

## Evidence

📸 **theHarvester Baidu Screenshot**

[Open `theharvester-baidu.jpg`](evidence/theharvester-baidu.jpg)

---

# 8. 🕵️ theHarvester — Multiple Sources

## Objective

A broader theHarvester search was performed against multiple available sources.

## Command

```bash
theHarvester -d networkwalks.com -l 50 -b all
```

## Results

The tool attempted to query many public information sources.

Several providers could not be queried because API credentials were missing or invalid.

Examples included services requiring API keys such as:

* Censys
* GitHub
* Hunter
* Shodan
* VirusTotal
* SecurityTrails
* ProjectDiscovery
* IntelX
* and other providers

The output also reported successful processing of several sources.

### Hudson Rock

The output reported:

```text
Domain statistics: 100 total compromised,
0 employees,
100 users
```

However, the subsequent search returned:

```text
0 hosts
0 IPs
0 emails
0 stealers
```

## Security Relevance

Using multiple OSINT providers can increase reconnaissance coverage.

However, results depend on:

* API availability
* Authentication
* Provider coverage
* Search-engine responses
* Data freshness
* Tool functionality

Therefore, missing results should be treated as **limitations**, not proof that no information exists.

## Evidence

📸 **theHarvester Multi-Source Screenshot**

[Open `theHarvester.jpg`](evidence/theHarvester.jpg)

---

# 📊 Findings Summary

| # | Finding                     | Observation                                                                     | Risk   |
| - | --------------------------- | ------------------------------------------------------------------------------- | ------ |
| 1 | Technology fingerprinting   | WordPress, WordPress Download Manager, Apache and other technologies identified | Medium |
| 2 | Public IP address           | `192.232.216.135` identified                                                    | Low    |
| 3 | HTTP information exposure   | Apache and WordPress API information visible                                    | Low    |
| 4 | WAF identified              | ModSecurity detected                                                            | Low    |
| 5 | DNS information exposed     | NS, SOA, MX, A, TXT and SRV records identified                                  | Medium |
| 6 | WHOIS information available | Registrar, dates and domain status identified                                   | Low    |
| 7 | Public OSINT limitations    | Multiple providers required unavailable API credentials                         | Low    |
| 8 | Subdomains discovered       | Three subdomains reported through DNS fallback                                  | Medium |

---

# 🧠 What I Learned

This exercise helped me understand how reconnaissance works before vulnerability exploitation begins.

### 1. Information gathering comes first

Before attempting to exploit a system, a security professional needs to understand the target environment.

### 2. Different tools reveal different information

No single reconnaissance tool provides a complete picture.

For example:

```text
WHOIS       → Domain information
WhatWeb     → Web technologies
Nslookup    → DNS → IP
Curl        → HTTP headers
Wafw00f     → WAF
DNSRecon    → DNS records
theHarvester → OSINT
```

### 3. Findings require interpretation

A discovered IP address, software version or DNS record should not automatically be classified as a vulnerability.

The information must be validated in context.

### 4. Tool limitations matter

TheHarvester demonstrated that modern OSINT tools may depend on external APIs and authentication.


# 🔐 Security Recommendations

Based on the reconnaissance observations, the following recommendations are proposed:

### 1. Review exposed technology information

Regularly review publicly visible technologies and versions.

### 2. Keep web technologies updated

Ensure WordPress, plugins and supporting technologies are maintained and patched.

### 3. Review HTTP headers

Remove unnecessary technical information where practical and maintain appropriate security headers.

### 4. Review DNS records

Regularly audit DNS records and remove obsolete or unnecessary entries.

### 5. Maintain the WAF

Keep ModSecurity appropriately configured, updated and monitored.

### 6. Review exposed subdomains

Investigate discovered subdomains and ensure every externally accessible service has a legitimate business purpose.

### 7. Validate OSINT findings

Information obtained from third-party intelligence providers should be independently validated before being treated as a confirmed security finding.


# 📄 Full Report

The complete professional report can be stored in:

```text
report/penetration-testing-report.pdf
```

**[📄 View Full Penetration Testing Report](report/penetration-testing-report.pdf)**
**[📄 View EVIDENT Penetration Testing Report](report/penetration-testing-report.pdf)**

---

# 🧪 Commands Used

For quick reference:

```bash
# WHOIS
whois networkwalks.com

# Web technology fingerprinting
whatweb networkwalks.com

# DNS resolution
nslookup networkwalks.com

# HTTP header inspection
curl -I https://networkwalks.com

# WAF detection
wafw00f networkwalks.com

# DNS enumeration
dnsrecon -d networkwalks.com

# theHarvester — Baidu
theHarvester -d networkwalks.com -l 1000 -b baidu

# theHarvester — multiple sources
theHarvester -d networkwalks.com -l 50 -b all
```

---

# 📚 References

* [GitHub Markdown Documentation](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
* [GitHub Repository README Documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories)
* [theHarvester — Official GitHub Repository](https://github.com/laramies/theHarvester)
* [theHarvester — Quick Start](https://github.com/laramies/theHarvester/wiki/Quick-Start)

TheHarvester's documentation confirms that it is designed for passive/public-source lookups and that provider availability and API credentials can affect which sources are usable.

---

# 👤 Author

**BRIAN MACHAYO**
#GITHUB
https://github.com/PrudenceMatrix/network-footprinting-assessment

#linkedIn
https://www.linkedin.com/in/brian-machayo


**Focus Areas:**

* 🔎 Reconnaissance
* 🌐 Network Security
* 🛡️ Defensive Security
* 🕵️ OSINT
* 🧪 Penetration Testing
* 🐧 Kali Linux

---

# ⭐ Portfolio Note

This project demonstrates practical experience with the **reconnaissance phase of a penetration-testing workflow**, including domain enumeration, DNS analysis, web technology fingerprinting, HTTP inspection, WAF identification and OSINT collection.

> **Educational Project — Authorized Security Testing Only**
