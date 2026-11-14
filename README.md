# 🕵️‍♂️ Penetration Testing Report: Network Traffic Analysis & OSINT

![Cybersecurity](https://img.shields.io/badge/Cybersecurity-Penetration_Testing-red?style=for-the-badge)
![Wireshark](https://img.shields.io/badge/Wireshark-Network_Forensics-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)
![OSINT](https://img.shields.io/badge/OSINT-Reconnaissance-green?style=for-the-badge)

**Author:** Nicholas Gyemfi (Cybersecurity Intern, Batch B084, Networkwalks)  
**Date:** 13 November 2026

## 📖 Overview
This repository documents a comprehensive penetration testing practical that covers two critical phases of an investigation: **Internal Network Traffic Analysis** (using Wireshark) and **External Reconnaissance & OSINT** (using nine industry-standard tools). 

Together, these exercises demonstrate how an analyst can gather intelligence from public sources on the outside, and how traffic captured on a network reveals what is really happening on the inside.

## 🛠️ Tools & Technologies Used
*   **Packet Analysis:** Wireshark (TCP/IP, HTTP/HTTPS, SIP, RTP)
*   **Reconnaissance:** WHOIS, WhatWeb, Nslookup, cURL, WAFW00F, DNSRecon
*   **OSINT:** Maltego, theHarvester, Google Dorking

## 🚀 Lab Activities Performed

### Phase 1: Network Traffic Analysis (Wireshark)
*   **Attacker Attribution:** Isolated suspicious IPs using Endpoint/Conversation statistics.
*   **TCP Stream Reconstruction:** Rebuilt fragmented packets to read full client-server interactions.
*   **Credential Exposure:** Extracted plaintext credentials from HTTP POST requests.
*   **Brute-Force Detection:** Correlated timestamps, ports, and source IPs to spot automated login attempts.
*   **VoIP Analysis:** Extracted SIP signaling and RTP streams to replay captured calls.

### Phase 2: Reconnaissance & OSINT (Exercises 02-10)
*   **Footprinting:** Used WHOIS for domain registration, Nslookup for DNS resolution, and cURL to inspect HTTP headers.
*   **Fingerprinting:** Utilized WhatWeb to identify CMS/plugins and WAFW00F to detect Web Application Firewalls.
*   **Enumeration:** Used DNSRecon to map out NS, MX, and TXT records.
*   **OSINT Mapping:** Leveraged Maltego and theHarvester to map public relationships, emails, and hosts. Used Google Dorking to surface exposed, unindexed data.

---

## 💡 Tricks & Tweaks (Pro-Tips from the Lab)
Here are the specific techniques used to overcome challenges during this engagement:

*   **Filtering the Noise:** When Wireshark captures are too dense, use `Statistics → Endpoints` and `Statistics → Conversations` to instantly identify which IPs are talking the most or using unusual ports.
*   **Reconstructing the Narrative:** Never analyze single TCP packets in isolation. Right-click and use **Follow → TCP Stream** to read the entire conversation. Red text is usually the client, blue is the server.
*   **The Magic HTTP Filter:** Use `http.request.method == "POST"` to instantly isolate login forms and submitted data.
*   **Decoding Brute-Forces:** Attackers often spread their attempts across different TCP connections to evade basic detection. You must correlate by *source IP, timestamp intervals, and destination port* across the whole capture.
*   **VoIP Forensics:** Don't just look at raw RTP packets. Go to **Telephony → VoIP Calls** to get a dedicated player, analyze jitter, and replay the audio stream.
*   **OSINT is a Puzzle:** Don't rely on one tool. Cross-reference WHOIS data with Nslookup IPs, and feed those domains into theHarvester and Maltego to build a complete picture of the target's external footprint.

## ⚠️ Risk Analysis & Findings
*   🔴 **Critical:** Plaintext credentials over HTTP (easily intercepted via TCP Stream).
*   🟡 **Medium:** Unencrypted application data and VoIP traffic (SIP/RTP).
*   🟡 **Medium:** Repeated authentication attempts (Brute-force susceptibility).
*   🟡 **Medium:** Sensitive data stored in raw packet captures.
*   🟢 **Low:** Difficulties in attacker attribution (IP alone is not enough).

## 🛡️ Recommendations
1.  Enforce **HTTPS/TLS** for all web traffic and **SIPS/SRTP** for VoIP.
2.  Implement **MFA** and rate-limiting to mitigate brute-force attacks.
3.  Secure packet captures and redact sensitive data before sharing.
4.  Retain network logs for accurate incident attribution.
5.  Conduct regular OSINT checks on your own organization to reduce your public attack surface.

## ⚠️ Disclaimer
*These activities were performed in an authorised lab environment and against a client (Networkwalks) with explicit written permission (Letter of Authorization NW-LOA-B084-017). No unauthorized access or exploitation was performed. All findings are for educational and defensive purposes.*

