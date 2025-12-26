# Web Attack Forensics - Drone Alone

# Walkthrough

- Open the web browser in the AttackBox and go to the following webpage: `http://MACHINE_IP:8000`
- Enter the following login information to access Splunk:`Blue:Pass1234`
- To modify the duration of the events in the Splunk interface, click the button to the left of the green magnifying glass and choose "`All time.`”

### Answer the questions below

What is the reconnaissance executable file name?

> `whoami.exe`
> 

```sql
index=windows_sysmon *cmd.exe* *whoami*
```

<aside>
💡

Looking at the Sysmon for other malicious executable files that the web server might have spawned, we can see that `httpd.exe` process ran `cmd.exe` which indicates a successful **command injection** and searching for above query, the below events confirms the attacker’s **post-exploitation reconnaissance.**

</aside>

![image.png](Web%20Attack%20Forensics%20-%20Drone%20Alone/image.png)

---

What executable did the attacker attempt to run through the command injection?

> `powershell.exe`
> 

```sql
index=windows_sysmon Image="*powershell.exe" (CommandLine="*enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*Base64*")
```

<aside>
💡

From the access logs, we can see that the attacker tries to execute system commands through a vulnerable CGI script (`hello.bat`) and trying to execute encoded command in powershell.

</aside>

![image.png](Web%20Attack%20Forensics%20-%20Drone%20Alone/image%201.png)