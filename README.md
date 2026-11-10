# NETWORKWALKS-RAVAHA-B084-WK2-PENETRATION-TESTING-REPORT

### Footprinting & Reconnaissance

**W2-PM-FINAL  |  CYBERSECURITY  |  NETWORKWALKS**

| Field | Detail |
|---|---|
| **Pentester Name (Cybersecurity Professional)** | **Ravaha-Tul-Hasan** |
| **Program/Batch** | B084-Networkwalks |
| **Date** | 10 november 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools)<br>W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (secured written permission already)<br>2. My own local LAN Network |
| **Permission secured from client?** | Yes |
| **Phases covered** | **Phase 1:** Reconnaissance & Footprinting<br>**Phase 2:** Scanning & Network Discovery<br>**Phase 3-5:** In Progress |

# 1. Liability Disclaimer

All activities described have been performed only on personally owned systems and devices or on those for which proper written permission was obtained.The information and materials provided are strictly intended for educational and research purposes. They must not be used for any illegal or unauthorized activities.The instructor, authors, and Networkwalks are not responsible for any misuse of this information. Every individual is solely responsible for their actions and any consequences that may arise.Unauthorized access to computer systems is a criminal offense in most countries, even if no damage is caused. Violations may result in criminal charges, substantial fines, job loss, and a permanent criminal record.Always act responsibly and ensure you have proper authorization before accessing or testing any system.

# 2. Introduction
This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning my own local LAN network with Zenmap (W2-PM5). First module covers the footprinting phase while the other module  covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. This is the second task (week 2) of my ongoing cybersecurity internship program at Networkwalks. All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed (scanning). Every step has been documented by their commands, screenshots and by their description for a simple explanation as to how things work.

# 3. Tools Applied

| Tools | Purpose |
|---|---|
Tools	Purpose
| Kali Linux & Windows | Operating systems used to perform network reconnaissance tasks.|
| WHOIS	               | Retrieve domain registration information, including ownership, registration dates, and name servers.|
| whatweb	             | Identifies website technologies such as web servers, CMS platforms, plugins, and IP addresses.|
| nslookup	           | Find the IP address associated with a domain through DNS lookup.|
| curl -I	             | Retrieve and examine a website's HTTP response headers.|
| wafw00f	             | Identify whether a website is protected by a Web Application Firewall (WAF).|
| dnsrecon	           | Gather DNS records, including NS, MX, SPF, TXT, and SRV records.|
| Zenmap               | (Nmap GUI)	Examine the local network to discover active devices, IP addresses, and MAC addresses.|
| Windows CMD	         | Check and identify the system's local IP and MAC addresses.|

# 4. Activities Handled

## 4.1 Footprinting & Reconnaissance

I performed reconnaissance on the networkwalks.com domain using six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl, Wafw00f, and DNSRecon. Each tool helped me collect a different type of information about the target website.

First, I used WHOIS to gather publicly available domain registration details and find the domain's name servers. This helped me understand basic information about the domain and its hosting setup.

Then, I used WhatWeb to identify the technologies used by the website and the results were WordPress 7.1.4 and WP Download Manager 3.3.76, along with other technical details.

Using Nslookup, I found the IP address linked to the domain which was 192.232.216.135.

I then used Curl with the -I option to view the website's HTTP response headers which gave me more details about the website and revealed the WordPress REST API endpoint /wp-json/.

Afterwards, I used Wafw00f to check whether the website was protected by a Web Application Firewall (WAF), it was protected by ModSecurity (SpiderLabs) WAF.

Finally, I used DNSRecon to collect information about the domain's DNS records. This gave me all details about name servers, mail servers, SPF/TXT records, service records, and DNS software information.

## 4.2 Network Scanning with Zenmap

For the second activity, I used **Zenmap** to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology. I first used the Windows `ipconfig` command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and clicked on ping scan to identify active hosts.

Listed below are 6 ip addresses in my local LAN network:

IP Address :-  
1. 192.168.0.1  
2. 192.168.0.33 
3. 192.168.0.35 
4. 192.168.0.37 
5. 192.168.0.38 
6. 192.168.0.46 

alongside their MAC addresses:

MAC Address :-
1. 40:92:49:68:12:C0
2. B4:0F:3B:FB:73:5F
3. 8A:CD:65:49:67:EC
4. 98:3B:8F:A3:9D:C8
5. Not listed
6. 42:D2:2D:6A:18:78

I then opened the topology section in Zenmap and saved it in PDF form as was instructed.

# 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| **\#** | **Risk / Finding**                           | **Evidence / Observation**                                  | **Potential Impact**                                                                                            | **Risk Level** |
|--------|----------------------------------------------|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|----------------|
| 1      | Web technology information exposed           | WhatWeb identified WordPress and WP Download Manager        | Attackers may use exposed technology/version information to identify software requiring further security review | **● Medium**   |
| 2      | Server IP address identifiable               | Nslookup resolved the domain to `192.232.216.135`           | Provides information about the network location of the web service                                              | **● Low**      |
| 3      | HTTP technical information exposed           | Curl returned HTTP response headers and exposed `/wp-json/` | May assist technology fingerprinting and further enumeration                                                    | **● Low**      |
| 4      | WAF technology identifiable                  | Wafw00f identified ModSecurity (SpiderLabs)                 | Reveals information about the web application’s security architecture                                           | **● Low**      |
| 5      | DNS infrastructure information exposed       | DNSRecon identified DNS, mail and service-related records   | DNS information can help build a broader infrastructure profile                                                 | **● Medium**   |
| 6      | Multiple live hosts visible on local network | Zenmap identified four live hosts in the example network    | Unknown or unauthorized devices may potentially be present on a network                                         | **● Medium**   |

**Risk level key:** ● Critical ● Medium ● Low

The risks mentioned above are based on observations from the footprinting and scanning activities. They are not confirmed vulnerabilities. The practical exercises mainly focused on gathering information and identifying active devices on the network. No exploitation or vulnerability testing was performed during these two modules. Therefore, finding information such as software versions, IP addresses, or DNS records does not automatically mean that a system is vulnerable. Further security testing with proper authorization would be needed to confirm any actual vulnerabilities.

# 6. Recommendations

The highly recommended practices are:

1. **Review publicly exposed technology information:** 
Organizations should regularly check what details about their website technologies, CMS platforms, and plugins can be seen publicly.

2. **Keep software updated:**
CMS platforms, plugins, and other website technologies should be updated regularly to fix security issues and stay protected against known threats.

3. **Review HTTP headers:**
HTTP response headers should be checked to make sure they do not reveal unnecessary technical details about the website.

4. **Review DNS records regularly:**
DNS records should be checked from time to time to ensure that only necessary information and services are available publicly.

5. **Properly configure and monitor the WAF:**
Ensure that the WAF (ModSecurity) remains enabled, properly configured, and regularly monitored to help block common attacks.

6. **Perform regular internal network discovery:**
Organizations should scan their internal networks regularly to find active devices and keep track of connected systems.

7. **Investigate unknown devices:**
Any unfamiliar or unexpected device found during a network scan should be checked to confirm whether it is authorized.

8. **Maintain network documentation:**
Keep records of network layouts and connected devices updated so that changes can be tracked easily.

9. **Perform security testing with authorization:**
Reconnaissance and scanning activities should only be carried out on systems and networks where proper permission has been granted.

# 7. Conclusion

During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical tasks related to footprinting, reconnaissance, and network scanning. For the footprinting activity, I used six Kali Linux tools to gather information about the target domain. I learned how WHOIS collects domain details, WhatWeb identifies website technologies, Nslookup finds IP addresses, Curl checks HTTP headers, Wafw00f detects Web Application Firewalls, and DNSRecon gathers DNS information. For the network scanning activity, I used Zenmap to examine my local network and find active devices. I also collected IP and MAC addresses and created a network topology to understand how devices were connected. These activities helped me understand the importance of information gathering in cybersecurity. Before attempting any security testing, professionals can learn a lot about a target by studying available information and network responses. I also learned how important proper documentation is in cybersecurity. A good report should clearly explain the activities performed, the findings, possible risks, and ways to reduce those risks. Lastly, I learned that reconnaissance and network scanning should always be carried out with proper permission and within an authorized scope. All these activities were completed as part of my assigned educational cybersecurity lab.

# 8. Evidences 

<img width="2543" height="1341" alt="whois" src="https://github.com/user-attachments/assets/3192a5e0-eacf-4d63-b6ea-73fe91057cc7" />

##

<img width="2558" height="1351" alt="whatweb" src="https://github.com/user-attachments/assets/c98d2ff9-2aef-4e17-b036-5947bd6f6f26" />

##

<img width="1438" height="957" alt="nslookup" src="https://github.com/user-attachments/assets/ff754bec-87ee-45a3-83c1-ea405ad7e503" />

##

<img width="2558" height="1202" alt="curl-I" src="https://github.com/user-attachments/assets/3e8cabcf-dbb9-4b0a-87bc-b21a161622ad" />

##

<img width="2558" height="1321" alt="wafwoof" src="https://github.com/user-attachments/assets/fa859e2b-bc20-403e-b325-eb441521ea7a" />

##

<img width="2558" height="1343" alt="dnsrecon" src="https://github.com/user-attachments/assets/37725488-eaa8-4eca-877d-91f3b83bbc42" />

##

<img width="1445" height="768" alt="ip graphics" src="https://github.com/user-attachments/assets/626562ea-76d6-4d51-8802-e3d68fab6fdb" />

##

<img width="1347" height="660" alt="zenmap" src="https://github.com/user-attachments/assets/ecc7cf53-b0f1-46d4-bfab-4b394ee78793" />

##

Ravaha-Tul-Hasan | Cybersecurity week 2 | Footprinting and Recon.
