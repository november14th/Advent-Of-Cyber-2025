# Phishing Phishmas Greetings

# Walkthrough

### Answer the questions below

Classify the 1st email, what's the flag?

> `THM{yougotnumber1-keep-it-going}`
> 
- **Spoofing, Sense of Urgency, Fake Invoice**

<aside>
💡

Highlights failed authentication (SPF/DKIM/DMARC fail) and mismatched Return-Path, proving sender forgery. Urgency via invoice pushes quick action. Classic business email compromise (BEC) style. 

</aside>

---

Classify the 2nd email. What's the flag?

> `THM{nmumber2-was-not-tha-thard!}`
> 
- **Impersonation, Spoofing, Malicious Attachment**

<aside>
💡

Disguised .html attachment (likely a phishing page) and full header failures confirming spoofing of "tbfc.com". Return-Path reveals true origin.

</aside>

---

Classify the 3rd email. What's the flag?

> `THM{Impersonation-is-areal-thing-keepIt}`
> 
- **Impersonation, Social Engineering Text, Sense of Urgency**

<aside>
💡

Direct impersonation of "McSkidy" using a personal Gmail address. No complex spoofing needed—relies on trust and urgency phrasing ("URGENT," "immediately").

**`Subject`:** URGENT: McSkidy VPN access for incident response

`From`: McSkidy <mcskiddyy202512@gmail.com>

</aside>

---

Classify the 4th email. What's the flag?

> `THM{Get-back-SOC-mas!!}`
> 
- **Impersonation, External Sender Domain, Social Engineering Text**

<aside>
💡

Clever use of legitimate service (Dropbox) for credibility. Mismatch between From/Reply-To/Return-Path exposes impersonation of "TBFC HR".

**`From`:** TBFC HR Department <no-reply@dropbox.com>
**`Reply-To` :** hr.tbfc@outlook.com
**`Return-Path`:** 345675444334263@email.dropbox.com

</aside>

---

Classify the 5th email. What's the flag?

> `THM{It-was-just-a-sp4m!!}`
> 
- **Spam**

<aside>
💡

All authentication passes, no malice. Serves as a "control" to teach distinguishing threats from noise.

</aside>

---

Classify the 6th email. What's the flag?

> `THM{number6-is-the-last-one!-DX!}`
> 
- **Impersonation, Typosquatting/Punycodes, Social Engineering Text**

<aside>
💡

The displayed From address shows "[tbƒc.com](http://xn--tbc-n5a.com/)" (where "ƒ" is likely U+0192 Latin small letter F with hook, or a similar homograph like Cyrillic). This visually mimics "[tbfc.com](http://tbfc.com/)" but encodes to a different Punycode domain (e.g., something like xn--tbc-something). The Return-Path reveals the true malicious domain (xn—[tbc-n5a.com](http://tbc-n5a.com/), possibly a variant). Combined with a tempting OneDrive link—advanced homograph attack to bypass visual inspection.

</aside>