 ![[Pasted image 20260601190659.png]]

# Hash Values (Trivial)
A hash value is a fixed-length unique value created from data using a hashing algorithm. It is used to identify files and data.

Some common hashing algorithms are:

- **MD5 (Message Digest)** – Created by Ron Rivest in 1992. It produces a 128-bit hash value. MD5 is no longer considered secure because attackers can create different files with the same hash value (called a hash collision).

- **SHA-1 (Secure Hash Algorithm 1)** – Developed by the NSA in 1995. It creates a 160-bit hash value shown as a 40-character hexadecimal string. SHA-1 is also no longer secure because it is vulnerable to brute-force attacks. NIST stopped recommending its use and suggested moving to stronger algorithms.

- **SHA-2** – Developed by NIST and NSA in 2001 as a replacement for SHA-1. One popular version is **SHA-256**, which creates a 256-bit hash value shown as a 64-character hexadecimal string. SHA-2 is much more secure and widely used today.

A hashing algorithm is not considered secure if two different files can generate the same hash value.

Security professionals use hash values to identify malware, suspicious files, and malicious artifacts. Hashes help analysts quickly recognize and track threats.

In ransomware and malware reports, researchers often include file hashes at the end of the report so others can identify the same malicious files.

Online tools like [VirusTotal](https://www.virustotal.com/?utm_source=chatgpt.com) and [OPSWAT MetaDefender Cloud](https://metadefender.opswat.com/?utm_source=chatgpt.com) can be used to perform hash lookups and analyze suspicious files.

# IP address
An IP address is used to identify devices connected to a network, such as computers, servers, and CCTV cameras. Devices use IP addresses to send and receive information over the internet or a network.

In the Pyramid of Pain, IP addresses are shown in green because they are easy for attackers to change.

From a defender’s perspective, knowing the IP addresses used by attackers is useful. Security teams often block or deny connections from malicious IP addresses using firewalls. However, this method is not very strong because attackers can easily switch to a new public IP address.

Attackers use different techniques to avoid IP blocking. One common technique is called **Fast Flux**.

Fast Flux is a DNS technique used by botnets to hide malicious activities such as:

- Phishing
- Malware delivery
- Web proxying
- Communication with command and control (C&C) servers

In a Fast Flux network, a single domain name is linked to many different IP addresses that constantly change. These IP addresses are usually compromised devices acting as proxies.

The main purpose of Fast Flux is to make it difficult for security professionals to detect and block the attacker’s infrastructure and communication channels.

Because attackers can quickly change IP addresses, blocking IPs alone causes very little pain to the attacker in the Pyramid of Pain.

# Domain Name
In the Pyramid of Pain, Domain Names are above IP addresses because they are slightly harder for attackers to change. The color changes from green to teal to show increased difficulty for the attacker.

A domain name maps an IP address to a readable text name, such as:

- evilcorp.com
- tryhackme.evilcorp.com

Attackers use malicious domains for phishing, malware delivery, and command-and-control (C2) communication.

Compared to changing an IP address, changing a domain name requires more effort because attackers usually need to:

- Purchase or register a new domain
- Configure DNS records
- Update their infrastructure

However, many DNS providers make this process easier by offering APIs and quick domain registration services.

One common attack involving malicious domains is the **Punycode attack**.

Punycode is a method that converts Unicode characters into ASCII format so browsers can display international domain names.

Attackers abuse this by creating domains that look similar to legitimate websites. For example:
- Legitimate domain: adidas.de
- Malicious lookalike: adıdas.de

The malicious version uses special Unicode characters that visually resemble normal letters. Its encoded Punycode version looks like this:

```txt
xn--addas-o4a.de
```

Modern browsers like:
- Google Chrome
- Microsoft Edge
- Safari

can often detect and display the full Punycode domain to help users notice suspicious websites.

Attackers also hide malicious links using URL shorteners. These services create short URLs that redirect users to another website.

Common URL-shortening services include:
- bit.ly
- tinyurl.com
- goo.gl
- ow.ly

You can sometimes preview the destination of a shortened link by adding a “+” at the end of the URL.

Security professionals detect malicious domains using:
- Proxy logs
- Web server logs
- DNS logs
- Sandboxing platforms

A popular malware analysis sandbox is [ANY.RUN](https://any.run/?utm_source=chatgpt.com). It allows analysts to observe malware behavior safely.

In ANY.RUN, analysts can review:
- **HTTP Requests**  
    Shows files or resources downloaded from a server, such as malware payloads or callbacks.
- **Connections**  
    Shows communication between the infected machine and other hosts, including possible C2 traffic or file transfers.
- **DNS Requests**  
    Shows domains the malware tries to contact. Malware often checks internet connectivity or communicates with command-and-control servers using DNS.

Analysts should never directly visit suspicious domains or IP addresses because they may host malware or phishing pages.

Since attackers can quickly create or change domains, blocking domains causes more pain than blocking IP addresses, but it is still not extremely difficult for attackers to adapt.

# Host Artifacts
In the Pyramid of Pain, Host Artifacts are in the yellow zone. At this level, attackers start feeling more pressure because detecting these artifacts forces them to change their tools, techniques, or attack methods.

Unlike IP addresses or domains, host artifacts are harder for attackers to modify. Changing them often requires rebuilding malware, rewriting code, or changing the way the attack works. This takes time, effort, and additional resources.

Host artifacts are traces or evidence left behind on a system during an attack. These artifacts help security professionals identify malicious activity.

Examples of host artifacts include:
- Registry changes or suspicious registry keys
- Unusual process execution
- Files dropped by malware
- Scheduled tasks created by attackers
- Suspicious PowerShell commands
- Malware persistence mechanisms
- Attack patterns and Indicators of Compromise (IOCs)

For example, if malware always creates a file in:

```txt
C:\Windows\Temp\malware.exe
```

security teams can detect or block this behavior.

Another example is detecting suspicious PowerShell activity:

```txt
powershell.exe -EncodedCommand
```

These behaviors are more difficult for attackers to hide because they are related to how the malware operates on the system.

Security tools such as:
- EDR (Endpoint Detection and Response)
- Antivirus software
- SIEM platforms
- Sysmon logs
are commonly used to detect host artifacts.

Detecting host artifacts causes more pain to attackers because they must redesign parts of their malware or attack workflow instead of simply changing an IP address or domain name.

# Network
Network Artifacts are also part of the yellow zone in the Pyramid of Pain. Detecting them causes more trouble for attackers because they may need to change their tools, communication methods, or attack techniques. This gives defenders more time to detect and stop future attacks.

Network artifacts are traces of malicious activity found in network traffic. These artifacts help security analysts identify suspicious communications between infected systems and attacker infrastructure.

Examples of network artifacts include:
- User-Agent strings
- Command and Control (C2) communication
- Suspicious HTTP requests
- URI patterns
- Unusual DNS traffic
- HTTP POST requests used for data transfer

A **User-Agent** is information sent by a browser or application during an HTTP request. It tells the server what software or device is making the request.

Attackers sometimes use unusual or fake User-Agent strings that are different from normal traffic in an organization. These suspicious User-Agents can help analysts identify malware or malicious tools.

Network artifacts are usually analyzed using:
- PCAP files (packet capture files)
- IDS alerts (Intrusion Detection System alerts)
- Network monitoring tools

Common tools used for network analysis include:
- Wireshark
- TShark
- Snort

For example, analysts may inspect suspicious HTTP POST requests in captured network traffic to identify malware communication.

Using TShark, analysts can extract HTTP hosts and User-Agent strings with this command:

```bash
tshark --Y http.request -T fields -e http.host -e http.user_agent -r analysis_file.pcap
```

This command:
- Filters HTTP requests
- Displays the host being contacted
- Shows the User-Agent string
- Reads data from a PCAP file

By analyzing these network artifacts, security teams can detect malware behavior, identify attacker infrastructure, and create detection rules.

Compared to blocking IP addresses or domains, detecting network artifacts causes more pain to attackers because they often need to redesign their communication patterns or modify their malware behavior.

# Tools
At this level of the Pyramid of Pain, defenders become much stronger against attackers. Detecting the attacker’s tools causes serious problems for the adversary because changing or replacing tools requires time, money, and technical skills.

If attackers lose access to their tools or those tools are easily detected, they may need to:
- Create a completely new tool
- Find another tool with similar capabilities
- Learn how to use a different framework
- Modify existing malware to avoid detection

This makes the attack much more difficult and expensive.

Attackers use many kinds of malicious tools, including:
- Malicious macro documents (maldocs)
- Backdoors for Command and Control (C2)
- Malicious EXE or DLL files
- Payloads
- Password crackers
- Information stealers

For example, malware may drop a suspicious file such as:

```txt
Stealer.exe
```

inside the Temp folder and execute it on the victim’s machine.

Security teams can detect these tools using:
- Antivirus signatures
- Detection rules
- YARA rules
- Threat intelligence feeds

YARA rules are commonly used to identify malware based on patterns, strings, or behavior found inside files.

Useful malware analysis and threat intelligence resources include:
- [MalwareBazaar](https://bazaar.abuse.ch/?utm_source=chatgpt.com)
- [Malshare](https://malshare.com/?utm_source=chatgpt.com)

These platforms provide:
- Malware samples
- Threat intelligence feeds
- YARA matches
- Malware analysis data

Security analysts also use detection rule platforms such as:
- [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/?utm_source=chatgpt.com)

where professionals share detection rules for malware, attacker behavior, and newly exploited vulnerabilities (CVEs).

Another important technique at this stage is **Fuzzy Hashing**.

Normal hashing only works if files are exactly the same. Even a small change creates a completely different hash.

Fuzzy hashing helps analysts compare files that are similar but not identical. This is useful because attackers often slightly modify malware to bypass traditional hash detection.

One common fuzzy hashing tool is:
- [SSDeep](https://ssdeep-project.github.io/ssdeep/index.html?utm_source=chatgpt.com)

SSDeep compares files and measures how similar they are based on fuzzy hash values.

Detecting attacker tools causes major pain because attackers must redesign, rebuild, or replace their malware and attack infrastructure instead of simply changing an IP address or domain.

# TTPs
TTPs (Tactics, Techniques, and Procedures) are the highest level in the Pyramid of Pain. This is the most difficult level for attackers to change and the most powerful level for defenders to detect.

TTPs describe the complete behavior and attack methods used by adversaries during an attack. This includes every stage of the attack, such as:
- Phishing emails
- Initial access
- Privilege escalation
- Persistence
- Credential dumping
- Lateral movement
- Data exfiltration

TTPs are heavily mapped in the:
- MITRE ATT&CK framework.

If defenders can quickly detect and respond to attacker behavior, attackers have very limited options to continue the attack.

For example, if a security team detects a:
- Pass-the-Hash attack

through Windows Event Log monitoring, they can quickly:
- Identify the compromised system
- Stop lateral movement
- Isolate infected hosts
- Prevent the attacker from spreading through the network

At this stage, attackers usually have only two choices:
1. Go back, perform more research, retrain, and redesign their tools and techniques
2. Give up and move to another target

The second option is often easier and less expensive for attackers.

This is why TTP detection causes the highest level of pain in the Pyramid of Pain. Unlike changing an IP address, domain, or malware file, changing attack behavior requires significant effort, planning, and expertise.

Modern security teams focus heavily on:
- Behavioral detection
- Threat hunting
- EDR/XDR monitoring
- SIEM correlation rules
- MITRE ATT&CK mapping

because detecting attacker behavior is far more effective than only detecting simple indicators like hashes or IP addresses.