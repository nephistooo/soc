EMAIL PHISHING ANALYSIS REPORT (TICKET: INC-2026-001)

Analyst : Andra,

Investigation Date : 20 November 2026,

Sample File : sample-1.eml,

Status : Confirmed Phishing / Malicious,

---

1. Executive Summary

A suspicious incoming email was identified employing a phishing scam, impersonating Banco do Bradesco (Livelo), a major bank from Brazil. The email utilizes social engineering tactics to lure the victim into clicking a link that redirects to a fake website.

Analysis of the email header and body confirms that this email was NOT sent from the bank's official server, but rather from a cheap VPS (Virtual Private Server) that has been abused.

---

2. Header Analysis (Email Metadata)

· Subject: CLIENTE PRIME - BRADESCO LIVELO: Seu cartão...
· From (Display Name): BANCO DO BRADESCO LIVELO <banco.bradesco@atendimento.com.br>
· Return-Path (Original): root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06...
· Message-ID: <20230919183549.39DEA3F725@ubuntu-s-1vcpu-1gb...>
· Authentication Results: FAIL (SPF: temperror, DMARC: temperror)

Key Findings:

1. Spoofing: The attacker forged the sender name (From) to appear as an official bank.
2. Attacker Infrastructure: Based on the Return-Path and Message-ID headers, this email was sent from a cheap VPS server named ubuntu-s-1vcpu... (likely rented from a cloud provider such as DigitalOcean).
3. Authentication Failure: The receiving system failed to verify the sender server's identity (SPF/DMARC Error), which is a strong indicator that this email is forged.

---

3. Email Body Analysis (Body & Payload)

· Obfuscation Technique: The email body is encoded using Base64 to bypass spam filters (Anti-Spam Gateway).
· Social Engineering (Manipulation Tactics):
  · False Urgency: The email claims the victim has 92,990 THOUSAND POINTS that will expire TODAY (EXPIRAM HOJE).
  · Bait: Offers discounts up to 35% on credit card bills.
  · Call to Action: Provides a "Resgatar Agora" (Redeem Now) button to lure the victim into clicking.

---

4. Indicators of Compromise (IoCs)

This is a list of "evidence" that must be blocked by the IT/Network team:

· Malicious URL: hxxps://blog1seguimentmydomaine2bra[.]me/ (Defanged)
· Sender Infrastructure: ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 (VPS Server)
· Domain Extension: .me (Frequently used for cheap phishing sites)

---

5. Recommendations & Mitigation

1. Block URL: Add the domain blog1seguimentmydomaine2bra.me to the company's firewall/proxy blocklist.
2. Delete Email: Remove the email from the user's inbox.
3. Education: Provide reminders to employees not to panic easily when receiving emails about "expiring points" or "huge discounts".
4. Follow-up Check: If the victim has already clicked and entered their data, immediately perform a Password Reset and enable MFA.

---

6. Evidence / Appendices

A. Email Header Analysis (SPF/DMARC Fail)
evidence/header_fail.png

B. Base64 Decoded Payload
evidence/decoded_body.png

C. Malicious URL Discovery
evidence/malicious_url.png

---

 Final Conclusion

This email is confirmed as Phishing with a High severity level. The email uses basic but effective techniques (urgency and reward bait) to steal the victim's credentials.

---
