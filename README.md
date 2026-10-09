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

---

### The Table Below shows the Raw Log provided in the Log Management, here is the breakdown of the HTTP traffic for investigation:

|  **User-Agent:**  |  **Date:**  |  **Request URL:**  |  **Device Action:**  |  **Request Method:**  |  **POST Parameters:**  |  **HTTP Response Size:**  |  **HTTP Response Status:**  |
|  :---  |  :---  |  :---  |  :---  |  :---  |  :---  |  :---  |  :---  |
|  Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)  |  2022-02-28 19:45:00  |  https://172.16.17.15/get_user_info/  |  Permitted  |  POST  |  ?user_id=2  |  253  |  200  |
|  Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)  |  2022-02-28 19:45:43  |  https://172.16.17.15/get_user_info/  |  Permitted  |  POST  |  ?user_id=1  |  188  |  200  |
|  Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)  |  2022-02-28 19:46:14  |  https://172.16.17.15/get_user_info/  |  Permitted  |  POST  |  ?user_id=3  |  351  |  200  |
|  Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)  |  2022-02-28 19:47:37  |  https://172.16.17.15/get_user_info/  |  Permitted  |  POST  |  ?user_id=4  |  158  |  200  |
|  Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)  |  2022-02-28 19:48:01  |  https://172.16.17.15/get_user_info/  |  Permitted  |  POST  |  ?user_id=5  |  267  |  200  |


### Key Analytical Findings

• Suspicious **User-Agent:** The request uses an ancient User-Agent string corresponding to Internet Explorer 6.0 on Windows XP. This is a massive red flag in a modern production environment, strongly suggesting an automated scanner, exploit tool, or manual script spoofing the browser identity.

• Successful Response: The HTTP Response Status is 200 (OK) and the Device Action is Permitted, meaning the web application successfully processed the request and sent a response payload back to the attacker.

• Evidence of IDOR: The parameters ?user_id=1, ?user_id=2, ?user_id=3, ?user_id=4 and ?user_id=5 explicitly point to numeric accounts manipulation targeting users records via the /get_user_info/ endpoint.

---

<img width="988" height="504" alt="image" src="https://github.com/user-attachments/assets/346e2f65-1522-495e-94e8-069796ace5ad" />

Based on the above evidences gathered previously (Key Analytical Findings) the option is to click **Malicious.**

---

### * Click **Yes**

<img width="981" height="400" alt="image" src="https://github.com/user-attachments/assets/917e37f4-f91c-43fe-8cd1-6eb7a372c452" />


### Supporting Evidence

• Alert Rule Name: The original alert explicitly stated SOC169 - Possible IDOR Attack Detected.
• Traffic Evidence: The raw logs showed direct object parameters manipulation (?user_id=1, ?user_id=2, ?user_id=3, ?user_id=4 and ?user_id=5) targeting the private user information endpoint (/get_user_info/), which is the definitive behavior of an Insecure Direct Object Reference exploit attempt.

---

<img width="1913" height="864" alt="image" src="https://github.com/user-attachments/assets/999e98b9-7860-4462-8395-91e38efb9891" />

The image above shows the Email Security dashboard on the LetsDefend platform, filtered for the date range 2023-07-25 to 2023-07-28. The screen states "There is no email to display" (0 emails).

This outcome is completely expected for this investigation. Because SOC169 is a web-based IDOR attack executing HTTP POST requests directly against a web server, the delivery mechanism bypasses email entirely.

Since there is no phishing component or email-based delivery vector to analyze here, you can safely confirm that no email artifacts exist for this incident.

---

<img width="998" height="461" alt="image" src="https://github.com/user-attachments/assets/838c8c48-bdf3-44cd-acd2-11223250fb38" />

* Click **Internet --> Company Network**
  * Because SOC169 is a web-based IDOR attack executing HTTP POST requests directly against a web server.

---

<img width="984" height="721" alt="image" src="https://github.com/user-attachments/assets/54cbfc0a-40ac-4907-859e-ed990c1de9df" />

<img width="1899" height="870" alt="image" src="https://github.com/user-attachments/assets/d3b8272a-60e0-46e5-b40b-6a65d4f94341" />

* Click **Yes**

<img width="996" height="375" alt="image" src="https://github.com/user-attachments/assets/f2675020-5995-4c02-a430-fff8a06808fc" />

---

### * The attack was successful based on the entries in the Log Management.

In web-application security alerts like IDOR, a "successful attack" does not require the attacker to gain command-line shell access, root privileges, or compromise the server's backend terminal. Because the raw log showed an HTTP 200 OK status code with several response body sizes of 253, 188, 351, 158 and 267 bytes when accessing ?user_id=1, ?user_id=2, ?user_id=3, ?user_id=4 and ?user_id=5 respectively, the application successfully processed the unauthorized requests and leaked the requested users data. The data exfiltration/privacy breach itself means the exploit succeeded.

---

<img width="980" height="691" alt="image" src="https://github.com/user-attachments/assets/ed1b67d0-fc7c-472c-9741-af1f4fae74db" />

• Go to Endpoint Security: Filter for the target server (172.16.17.15).
• Isolate the Host: Click the Request Containment button next to that device to cut off its network access and restrict further malicious activity.

<img width="1909" height="849" alt="image" src="https://github.com/user-attachments/assets/51a1ab9c-1f4f-4343-b6dd-133c9245ee20" />

---
### Key artifacts for the indicators of compromise (IoC) for this case.

• Value: 134.209.118.137
• Comment: Malicious source IP initiating IDOR attack
• Type: Select IP from the dropdown menu.

Click the "+" icon in the top left of the modal to add a second row, then enter the following details for the second artifact:
• Value: 172.16.17.15
• Comment: Targeted internal web server
• Type: Select IP from the dropdown menu.

<img width="986" height="574" alt="image" src="https://github.com/user-attachments/assets/7763c464-d1ad-4e5b-94e8-23df1b978b18" />

---

### * Select **Yes**

<img width="978" height="648" alt="image" src="https://github.com/user-attachments/assets/efc5c3dd-4b8a-4f74-a2d3-2b0e237f4af5" />

### Reasons Why Tier 2 Escalation is Required

• According to the escalation criteria card shown earlier: "In cases where the attack succeeds, Tier 2 escalation should be performed." Because the IDOR vulnerability successfully returned data to the attacker, senior analysts need to be notified to perform full data-impact assessments, coordinate with developers to patch the code, and notify affected users if necessary.

---

<img width="993" height="553" alt="image" src="https://github.com/user-attachments/assets/f849f94d-3390-4460-90a6-e6ae47df2fde" />

```
I investigated an alert for an IDOR (Insecure Direct Object Reference) attack targeting the internal web server (172.16.17.15) from an external cloud IP address (134.209.118.137) hosted on DigitalOcean infrastructure. 

Log management analysis revealed multiple inbound HTTP POST requests directed at the '/get_user_info/' endpoint using unauthorized numeric account parameters (?user_id=1, ?user_id=2, ?user_id=3, ?user_id=4 and ?user_id=5) alongside a spoofed User-Agent string (Internet Explorer 6 on Windows XP). The web application permitted these requests and returned an HTTP 200 OK response with these consistent payload sizes of 253, 188, 351, 158 and 267 bytes. This confirms that the attack successfully bypassed proper authorization checks and exposed sensitive user information at the application layer, classifying the incident as a True Positive. 

Because data exposure occurred, the host was determined to be compromised at the application level. Remediation and containment procedures were initiated immediately: network isolation was requested via the Endpoint Security console using the "Request Containment" feature to restrict the attacker, prevent further automated scanning, and limit operational impact. Tier 2 escalation has been performed for advanced impact analysis, data breach verification, and remediation coordination.

Remediation Recommended: Maintain host isolation until code review is complete. Implement strict server-side, object-level access controls checks on the '/get_user_info/' endpoint to ensure authenticated users can only access their own records. Permanently block the malicious source IP (134.209.118.137) on edge firewalls.

```

---

### **Click Confirm & Close** 

* To officially submit and close out this case (Ticket)

<img width="1010" height="442" alt="image" src="https://github.com/user-attachments/assets/3ee7f090-eb6c-4daa-8272-2f775319046f" />
<img width="807" height="583" alt="image" src="https://github.com/user-attachments/assets/77994452-5259-4761-ad67-b0bd27071422" />

---

### FINAL RESULTS 

<img width="1917" height="833" alt="image" src="https://github.com/user-attachments/assets/c39eb1c6-472b-4b31-98cf-15e9e16326f1" />
<img width="1900" height="505" alt="image" src="https://github.com/user-attachments/assets/66990f42-a0c8-445a-b711-aead302df829" />
<img width="1901" height="542" alt="image" src="https://github.com/user-attachments/assets/0bf58bd4-6037-44d4-8154-df574c97fa03" />
<img width="1915" height="339" alt="image" src="https://github.com/user-attachments/assets/aa8b5f20-0a2e-466e-8de3-e06ca60921e4" />

---
