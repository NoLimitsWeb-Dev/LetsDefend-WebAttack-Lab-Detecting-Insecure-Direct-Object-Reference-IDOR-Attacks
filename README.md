# LetsDefend-WebAttack-Lab-Detecting-Insecure-Direct-Object-Reference-IDOR-Attacks

## How to Detect and prevent different types of Web Attacks: SQL Injection,  Cross Site Scripting,  Command Injection,  IDOR,  RFI & LFI and File Upload (Web Shell)

## Practice with SOC Alerts
---
### 🔗119 - SOC169 - Possible IDOR Attack Detected
---

Here is My assigned Ticket, seating in my Investigation Channel; ready to be investigated
<img width="1917" height="631" alt="image" src="https://github.com/user-attachments/assets/27ed4d3b-469b-4670-81c1-fd73e3689d7b" />

---

* Click **Details** to view more information about the Ticket.

<img width="1899" height="900" alt="image" src="https://github.com/user-attachments/assets/9a474372-fc6a-4e76-86cd-0ecc076691cf" />

---

* Click >> Create Ticket to Create ticket for EventID: 119
* Click the blue **Continue** button to create a ticket
* Click **OK** when the window pops up "**Ticket Created**" indicating my "The ticket has been created successfully."
<img width="1919" height="616" alt="image" src="https://github.com/user-attachments/assets/4815d120-819b-4c6f-b1cf-898cc7187233" />

<img width="1061" height="403" alt="image" src="https://github.com/user-attachments/assets/caceb71c-b4c8-4e03-b954-9c9dbea3c5cb" />

---

### Play Book Opens
(Which is used to begin the guided incident response investigation for this specific Insecure Direct Object Reference (IDOR) alert.)

<img width="1911" height="606" alt="image" src="https://github.com/user-attachments/assets/829d6f35-c6bd-429b-b94e-0535f0b0df1e" />

This screen highlights a critical security alert:

• Incident Name: SOC169 - Possible IDOR Attack Detected

• Incident Type: Web Attack

• Created Date: 2026-10-09 12:27:56

The dashboard indicates that I am currently navigating within the Case Management section (highlighted on the left panel). 

* Click blue **Start Playbook!** button.

---

<img width="990" height="606" alt="image" src="https://github.com/user-attachments/assets/a9d3c848-a609-4c8a-9eb0-f96c1a251f7c" />

This step outlines the fundamental methodology required before analyzing logs directly to determine if the alert is a false positive or a true positive:

• Examining the rule name: SOC169 - Possible IDOR Attack Detected).

• Detected traffic communication: The source ```134.209.118.137``` and destination devices ```172.16.17.15``` (**Host Name: Webserver1005**)

This helps map out the direction of the traffic, the communication flow, and the specific network protocols used.

---

* Click **Log Management**
* Click **Basic**
* Type in One of the IoC"s eg. **Source IP Address:** ```134.209.118.137```

<img width="1911" height="892" alt="image" src="https://github.com/user-attachments/assets/aaa4b819-c128-4cc8-bdef-291560a34d63" />

* Result: It displays only the traffic between the source ```134.209.118.137``` and destination devices ```172.16.17.15``` (**Host Name: Webserver1005**)

<img width="1906" height="903" alt="image" src="https://github.com/user-attachments/assets/eceead9a-0530-4f74-89aa-6bf1d534c573" />

---

<img width="531" height="421" alt="image" src="https://github.com/user-attachments/assets/d29026fa-837a-41a5-9a2c-bf433f745b25" />

|  Source Port  |  Destination Port  |
|  :---  |  :---  |
|  Attacker  |  Victim  |
|  Ports Used: Typically high-numbered ephemeral ports 49211, 48523, 47274, 43461 and 49271.  |  Port Used: 443 (HTTPS).  |
|  Reputation: These are standard dynamic client-side ports generated automatically by the attacker's system to establish an outbound TCP connection.  |  Reputation: These are trusted, standard ports used globally to host public-facing websites and secure web communication.  |

---

<img width="977" height="683" alt="image" src="https://github.com/user-attachments/assets/9eda5fec-f5be-4f74-95cc-3807ac145417" />


### External Traffic Data (Internet IP Analysis)

• Ownership / ISP: DigitalOcean, LLC

• Usage Type: Data Center / Web Hosting / Transit

• Geographic Location: North Bergen, New Jersey, United States

---

<img width="1917" height="903" alt="image" src="https://github.com/user-attachments/assets/ebc29ac5-0f7b-4b9c-8a52-a20b8cf8ffbc" />

• VirusTotal Reputation: 0 / 92 Malicious Flags (Completely clean according to security vendors, though it holds a community score of -5).

---

<img width="1893" height="908" alt="image" src="https://github.com/user-attachments/assets/020bf249-302c-4ca6-88c7-aecc704b0be1" />
<img width="1907" height="828" alt="image" src="https://github.com/user-attachments/assets/e0571327-f9f4-4936-8ba6-1f7feda79ebf" />

• AbuseIPDB Reputation: 0% Abuse Confidence Score (Low Risk). While it has been reported 1,537 times historically, there are no reports in the last 60 days, indicating its abusive activity has decayed or stopped recently.

---

Summary Analysis:

The IP belongs to a public cloud provider/VPS infrastructure (DigitalOcean). While threat intelligence engines currently rate it as "clean" due to a lack of recent activity (last 60 days), its classification as a hosted data center IP makes it highly suspicious when initiating inbound web attacks, as threat actors frequently rent temporary cloud servers to launch automated exploit campaigns.

---

<img width="987" height="726" alt="image" src="https://github.com/user-attachments/assets/49734c43-5e8c-402d-8094-db7f0f1ddac5" />

|  Date: 2022-02-28 19:45:00  |  Request URL: https://172.16.17.15/get_user_info/  |  Device Action: Permitted  |  Request Method: POST  |  POST Parameters: ?user_id=2  |  HTTP Response Size:: 253  |  HTTP Response Status: 200  |
|  :---  |  :---  |  :---  |  :---  |  :---  |  :---  |  :---  |
