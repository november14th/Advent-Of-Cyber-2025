# Splunk Basics - Did you SIEM?

# Walkthrough

- First, we click the `Searching & Reporting` button in the upper-left corner of the page.
- Next, we enter `index=main` in the New search form at the top of the page.
- Finally, we click the button to the left of the green magnifying glass and choose `All time`.

### Answer the questions below

What is the attacker IP found attacking and compromising the web server?

> `198.51.100.55`
> 

<aside>
💡

Searching query `index=main sourcetype=web_traffic` , we see that the only external `client_ip` is `198.51.100.55` .

</aside>

---

Which day was the peak traffic in the logs? (Format: YYYY-MM-DD)

> `2025-10-12`
> 

<aside>
💡

Looking at the histogram, we can see that on `2025-10-12` , there was peak traffic.

</aside>

```sql
index=main sourcetype=web_traffic | timechart span=1d count | sort by count | reverse
```

---

What is the count of Havij user_agent events found in the logs?

> `993`
> 

```sql
index=main sourcetype=web_traffic user_agent="Havij/1.17 (Automated SQL Injection)"
```

---

How many path traversal attempts to access sensitive files on the server were observed?

> `658`
> 

```sql
index=main sourcetype=web_traffic path="*..*"
| stats count by path
```

---

Examine the firewall logs. How many bytes were transferred to the C2 server IP from the compromised web server?

> `126167`
> 

```sql
index=main sourcetype=firewall_logs dest_ip="198.51.100.55" 
|  stats sum(bytes_transferred) by src_ip
```