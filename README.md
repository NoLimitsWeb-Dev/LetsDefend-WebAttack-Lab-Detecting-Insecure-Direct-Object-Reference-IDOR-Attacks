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
|  Ports Used: Typically high-numbered ephemeral ports (e.g., above 1024 like 50000+ or 4433 depending on the specific log line).  |  Port Used: 443 (HTTPS).  |
|  Reputation: These are standard dynamic client-side ports generated automatically by the attacker's system to establish an outbound TCP connection.  |  Reputation: These are trusted, standard ports used globally to host public-facing websites and secure web communication.  |
