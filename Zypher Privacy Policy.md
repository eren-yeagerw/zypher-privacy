# PRIVACY POLICY

**Effective Date:** November 22, 2026  
**Last Updated:** November 22, 2026  

This Privacy Policy ("Policy") governs the collection, processing, storage, and disclosure of information by **Zypher** ("the Bot," "Service," "we," "us," or "our"), a security, moderation, and utility application operating on the Discord platform. 

By inviting Zypher to a Discord server ("Guild"), configuring its modules, or interacting with its commands and automated systems, you ("User," "Server Administrator," or "Data Subject") acknowledge that you have read, understood, and agreed to the data practices described in this Policy. If you do not consent to these terms, you must immediately remove Zypher from your server and cease all use of the Service.

---

## 1. DEFINITIONS

For the purposes of this Policy:
* **"Discord"** refers to Discord Inc. and its proprietary communication platform and Application Programming Interfaces (APIs).
* **"Guild" or "Server"** refers to a virtual community space hosted on Discord where Zypher is authorized to operate.
* **"Ephemeral Processing"** refers to the transient inspection or caching of data strictly within volatile memory (Random Access Memory / RAM) without persistent disk or database storage.
* **"Personal Data"** refers to any information relating to an identified or identifiable natural person, including Discord User IDs and user-generated content.

---

## 2. CATEGORIES OF DATA COLLECTED AND PROCESSED

Zypher adheres to the principle of data minimization, collecting and processing only the information strictly necessary to execute its security, moderation, and utility functions.

### 2.1 Persistent Server Configuration Data
When Zypher is added to a Guild or configured by authorized administrators, we store the following metadata in our persistent database:
* **Guild Identifiers:** Guild ID, Guild Owner ID, custom command prefixes, and designated security/moderation log channel IDs.
* **Security & Module Parameters:** Configurations for **AutoMod** (custom word blacklists, link filters, spam thresholds, and Anti-Scam filter toggles), **Anti-Nuke** (action rate limits, trusted/whitelisted User and Role IDs, and automated punishment triggers), and **Panic Mode** (designated lockdown channels and permission override states).
* **Moderation Case Records:** Logs of executed moderation actions (bans, kicks, timeouts, warnings), limited to target User IDs, executing Moderator/System IDs, action reasons, and timestamps.

### 2.2 Real-Time Message Content Monitoring (Prefix Commands & AutoMod)
To support traditional prefix-based commands and real-time threat mitigation, Zypher utilizes Discord’s `MESSAGE_CONTENT` privileged intent under the following strict conditions:
* **Prefix Command Execution:** Zypher monitors incoming message text in real time solely to detect whether a message begins with the Guild's configured command prefix (or mentions the Bot). Messages that do not match a valid command prefix and do not trigger an active AutoMod rule are immediately discarded from memory without logging, indexing, or retention.
* **AutoMod Text & Link Inspection:** Incoming messages are analyzed instantaneously in volatile memory against configured spam rules, mass-mention limits, blacklisted phrases, and known phishing domains. **Zypher does not maintain permanent archives or databases of general server chat history.**

### 2.3 Anti-Scam Image Analysis (Local OCR & Machine Learning)
When the **Anti-Scam** module is enabled in a Guild, Zypher inspects image attachments and embedded media posted in monitored channels:
* **Local On-Server Processing:** Images are downloaded temporarily into isolated, volatile memory (RAM) on our dedicated infrastructure and analyzed using **local Optical Character Recognition (OCR)** and an **in-house machine learning classification model** to detect fraudulent text, cryptocurrency scams, phishing overlays, or malicious QR/visual patterns.
* **Zero Third-Party AI Sharing & Immediate Purge:** Image files and extracted OCR text are **never transmitted to external third-party AI APIs** and are **never retained for model training or storage**. Immediately upon completion of the scam classification check (typically within milliseconds), the image buffer and extracted text are permanently purged from memory.

### 2.4 Anti-Nuke & Panic Mode Audit Telemetry
To safeguard Guilds against unauthorized administrative destruction, raids, and malicious compromises, Zypher continuously monitors Discord Gateway events and Audit Logs:
* **Action Rate Tracking:** Zypher tracks high-risk administrative actions—including channel creations/deletions, role modifications/deletions, mass member bans/kicks, webhook creations, and permission escalations—associated with the executing User ID.
* **Automated Lockdown Execution:** Threshold counters are held ephemerally in volatile memory to trigger Anti-Nuke countermeasures or **Panic Mode** (automated server-wide channel lockdowns).

### 2.5 Ephemeral & On-Demand Utility Data
* **Snipe Module (5-Minute Ephemeral Cache):** When a message is deleted in a Guild where the `snipe` module is active, Zypher temporarily caches the deleted message content, attachment proxy URLs (if applicable), author User ID, and deletion timestamp in volatile memory (RAM) for a strict maximum duration of **five (5) minutes**. Upon expiration of the 5-minute window, or upon cache overwrite/clearance, the data is irreversibly purged.
* **Avatar, Banner, and General Utility Commands:** When users invoke commands such as `avatar`, `banner`, or general informational utilities, Zypher queries Discord’s API on demand to retrieve publicly accessible profile metadata (User ID, username, avatar hash/URL, and banner hash/URL). **Such media and profile attributes are not persisted in our databases.**

---

## 3. LEGAL BASIS AND PURPOSE OF PROCESSING

We process data strictly for the following legitimate and contractual purposes:
1. **Service Delivery & Security Enforcement:** Executing user-invoked prefix/slash commands, enforcing AutoMod and Anti-Scam protections, mitigating server nukes, and executing Panic Mode lockdowns.
2. **System Integrity & Abuse Prevention:** Monitoring command rate limits, preventing denial-of-service attacks against Zypher, and debugging operational errors.
3. **Compliance with Platform Policies:** Ensuring adherence to the Discord Developer Terms of Service and Developer Policy.

**Commercial Prohibition:** We do **not** sell, rent, lease, trade, or monetize User Personal Data, message contents, OCR outputs, or Guild metadata to any third party, data broker, or advertising network.

---

## 4. DATA RETENTION AND AUTOMATIC DELETION SCHEDULE

Zypher enforces strict automated data lifecycle policies:

| Data Category | Storage Medium | Retention Period | Deletion Mechanism |
| :--- | :--- | :--- | :--- |
| **Guild Configurations & Whitelists** | Encrypted Database | Active while in Guild + **7 Days** post-removal | Automatically and permanently purged **7 days** after Zypher is removed/kicked from a Guild, unless Zypher rejoins within that 7-day grace period. |
| **Snipe Deleted Message Cache** | Volatile Memory (RAM) | Maximum **5 Minutes** | Automatically evicted upon TTL expiration, cache overwrite, or administrator clear command. |
| **Anti-Scam Images & OCR Output** | Volatile Memory (RAM) | **Milliseconds** (Processing duration only) | Immediately overwritten and garbage-collected post-inference. |
| **Prefix Command & AutoMod Message Streams** | Volatile Memory (RAM) | **Milliseconds** (Real-time inspection) | Discarded immediately if non-command / non-violating. |
| **Anti-Nuke Rate Counters** | Volatile Memory (RAM) | **Seconds to Minutes** | Automatically cleared upon rate-window expiration. |

---

## 5. DATA SECURITY AND INFRASTRUCTURE

We implement industry-standard technical and organizational safeguards to protect stored configuration data against unauthorized access, alteration, disclosure, or destruction:
* **Encryption:** All network communications between Zypher, Discord’s API, and our database clusters are encrypted in transit via TLS 1.2/1.3, and persistent database volumes are encrypted at rest.
* **Access Controls:** Production servers and databases are protected by strict firewall rules, SSH key authentication, and role-based access control limited exclusively to authorized core developers.
* **Data Isolation:** OCR and machine learning inference for the Anti-Scam filter are executed locally within our secured compute environment, eliminating external data exposure risks.

---

## 6. THIRD-PARTY SERVICES

Zypher operates exclusively on the **Discord** platform. Any interaction with Zypher is simultaneously subject to Discord’s [Privacy Policy](https://discord.com/privacy) and [Terms of Service](https://discord.com/terms). 

We utilize reputable cloud infrastructure providers solely for hosting Zypher’s compute instances and encrypted databases. No third-party analytics trackers, external AI processors, or advertising SDKs are integrated into the Bot.

---

## 7. USER RIGHTS AND DATA SUBJECT CONTROLS

In accordance with applicable data protection laws—including the General Data Protection Regulation (GDPR), the California Consumer Privacy Act (CCPA/CPRA), and India’s Digital Personal Data Protection Act (DPDP Act, 2023)—Users and Server Administrators possess the following rights:

1. **Right to Erasure ("Right to be Forgotten"):**
   * **Server-Level Deletion:** Server Administrators may delete all Guild configuration data by removing Zypher from the server (triggering automatic permanent erasure after **7 days**) or by executing the Bot's configuration reset commands.
   * **User-Level Deletion:** Individual users may request the erasure of any persistent identifiers (such as moderation log entries or whitelisted IDs) associated with their Discord User ID by contacting us via the channels in Section 10.
2. **Right of Access & Portability:** You may request a summary of any persistent data stored by Zypher linked to your Discord User ID or owned Guild ID.
3. **Right to Restrict Processing:** Server Administrators may selectively disable specific modules (including `snipe`, `antiscam`, or `automod`) at any time via Zypher’s configuration commands.

Verified data access or deletion requests will be fulfilled within **fourteen (14) calendar days**.

---

## 8. CHILDREN'S PRIVACY

Zypher is not directed toward, nor intended for use by, individuals under the minimum legal age required to use Discord in their respective jurisdiction (13 years of age or older, or higher where mandated by local law). We do not knowingly collect or maintain Personal Data from individuals below the applicable age of digital consent. If we become aware that data belonging to an underage individual has been inadvertently stored, we will purge it promptly.

---

## 9. AMENDMENTS TO THIS POLICY

We reserve the right to modify or update this Privacy Policy at any time to reflect changes in Zypher’s functionality, security architecture, or applicable legal obligations. Material updates will be indicated by revising the **"Last Updated"** date at the top of this Policy and publishing a notice within Zypher’s official Discord Support Server. Continued use of Zypher following such updates constitutes acceptance of the revised Policy.

---

## 10. CONTACT INFORMATION

For privacy inquiries, security disclosures, or requests to exercise your data protection rights, please contact the Zypher administration team:

* **Official Support Server:** [Insert Discord Support Server Invite Link]
* **Privacy & Legal Contact Email:** [Insert Contact Email Address]
* **Official Website / Documentation:** [Insert Website URL, if applicable]