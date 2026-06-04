# Phishing Detection & Awareness System

## 📌 Project Overview
This project is an industry-grade Security Awareness Asset developed during my Cyber Security Internship with **Future Interns**. The goal of this project is to analyze a real-world phishing email targeting Microsoft account credentials, break down the technical threat indicators from raw email headers, and provide an actionable corporate defense manual that non-technical corporate employees can easily understand.

---

## 🛠️ Tools & Approach Used
* **Header Analysis Tools:** Google Admin Toolbox MessageHeader / MXToolbox (Used to parse raw email headers and identify spoofing).
* **Link Inspection:** Safe Browser Sandbox URL Inspection (To identify deceptive reply-to forms and missing protocols).
* **Documentation:** Microsoft Word / Google Docs (Formatted with user-friendly scannability and professional typography).

---

## 📁 Repository Contents
* `Phishing_Detection_and_Awareness_Report.pdf` - The complete corporate awareness and technical breakdown report.
* `phishing_email_sample.txt` - The raw email headers and HTML bait source used as evidence for this analysis.

---

## 🔍 Case Study: Microsoft Account Unusual Sign-In Activity Phishing

### 📥 The Bait (Email Summary)
- **Subject Line:** `Microsoft account unusual signin activity`
- **Visual Presentation:** Mimics an official Microsoft Security notification alerting the user of an unauthorized login from **Russia/Moscow (IP: 103.225.77.255)** using Firefox on Windows 10.
- **The Call to Action:** A prominent blue button labeled **"Report The User"** designed to trigger fear and prompt an immediate click.

---

## 🕵️‍♂️ Technical Dissection & Red Flags (How I Caught the Scam)

### 🚩 1. Spoofed Sender Display vs. Actual Return Path
* **Display Name:** `Microsoft account team`
* **From Header Address:** `<no-reply@access-accsecurity.com>` (A lookalike domain registered by attackers to appear legitimate).
* **Actual Source (`Return-Path`):** `bounce@nonkfrgr.co.uk` 
* **Analysis:** The actual server delivering the mail belongs to a completely unrelated UK domain (`nonkfrgr.co.uk`), which is a definitive sign of sender spoofing.

### 🚩 2. Authentication Failures (SPF, DKIM, DMARC)
Looking at the raw authentication markers in the header:
* `Received-SPF: None` (`nonkfrgr.co.uk` does not designate permitted sender hosts).
* `dkim=none` (The message was completely unsigned, which never happens with legitimate Microsoft infrastructure).
* `dmarc=permerror action=none header.from=access-accsecurity.com`
* **Analysis:** The sending IP (`89.144.9.87`) failed validation checks, proving the email originated from an unauthorized mail server.

### 🚩 3. Deceptive Reply-To Mechanism
* `Reply-To: solutionteamrecognizd02@gmail.com`
* **Analysis:** Official Microsoft alerts will never ask you to reply to a free, public `@gmail.com` address. If an employee clicks "Report The User," it forces their email client to send account data directly to the hacker's personal Gmail inbox.

### 🚩 4. Obfuscation & Hidden Tracking Pixels
* **Hidden Tracking:** At the bottom of the HTML code, a hidden `1px x 1px` invisible image tracker is embedded: 
  `src="http://thebandalisty.com/track/..." style="visibility:hidden"`
* **Analysis:** Attackers use this to silently track whether the employee opened the email, confirming that the email address is active for future attacks.
* **Code Stuffing:** The email body includes massive blocks of hidden CSS styles containing random scrambled words (`nergie b326`, `tweeting pbt85voo_pm`, etc.) to intentionally bypass automated corporate spam filters.

---

## 📊 Threat Classification & Risk Assessment

| Parameter | Assessment | Details |
| :--- | :--- | :--- |
| **Threat Type** | Credential Harvesting / Social Engineering | Traps the user into revealing email credentials under artificial panic. |
| **Risk Category** | **CRITICAL** 🔴 | High probability of bypassing weak filters due to anti-spam obfuscation techniques. |
| **SCL Score** | `SCL: 5` (Spam Confidence Level) | In the header, Exchange correctly tagged this message with a high spam confidence rating. |

---

## 💡 The 3-Second Mental Checklist for Employees
Every time you open a security alert email, ask yourself these three quick questions before clicking anything:
1. **Was I expecting this?** (Did I actually try to log in or modify my account just now?)
2. **Is it rushing me?** (Is it showing a random login from another country to scare me into taking immediate action?)
3. **Where does the button point?** (If I hover over the action button, does it point to `microsoft.com` or a random Gmail/external address?)

> 🚨 **Golden Rule:** If the email fails even **one** of these questions, stop. Do not click. Use the **"Report Phishing"** button in your mail client immediately!

---

## 👥 Connect with Me
* **Organization:** Developed for **Future Interns** Cyber Security Program.
* **LinkedIn:** www.linkedin.com/in/ritika-karak-b190833b0
