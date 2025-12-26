# Network Discovery - Scan-ta Clause

# Walkthrough

---

Here, the target is `tbfc-devqa01` server with the `10.80.156.231` address. First we scan the top 1000 most commonly port using `nmap`.

```sql
└─$ nmap 10.80.156.231           
Starting Nmap 7.95 ( https://nmap.org ) at 2025-12-09 01:46 EST
Nmap scan report for 10.80.156.231 (10.80.156.231)
Host is up (0.18s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

We can either access SSH port if we know the password or access an HTTP website using `http://10.80.156.231`

### Answer the questions below

What evil message do you see on top of the website?

> `Pwned by HopSec`
> 

![Website](Network%20Discovery%20-%20Scan-ta%20Clause/image.png)

Website

---

What is the first key part found on the FTP server?

> `3aster_`
> 
- Since we only scanned top 1000 most commonly used ports, we need to scan whole range i.e. 65535 ports where other services can hide.
    
    ```bash
    $ nmap -p- --script=banner 10.80.156.231
    PORT      STATE SERVICE
    22/tcp    open  ssh
    |_banner: SSH-2.0-OpenSSH_9.6p1 Ubuntu-3ubuntu13.14
    80/tcp    open  http
    21212/tcp open  trinket-agent
    |_banner: 220 (vsFTPd 3.0.5)
    25251/tcp open  unknown
    |_banner: TBFC maintd v0.2\x0AType HELP for commands.
    ```
    
    <aside>
    💡
    
    `-p-` argument to scan all ports, and `--script=banner` to see what's likely behind the port.
    
    </aside>
    

- Looks like there is a running FTP server on port `21212` and some custom TBFC application on port **`25251`.** Let's try accessing the FTP in anonymous mode with the `ftp` command and see if we can find our way in!
    
    ```bash
    $ ftp 10.80.156.231 21212
    
    ftp> passive
    ftp> ls
    ftp> get tbfc_qa_key1
    ftp> exit
    
    ```
    
- Here, we enter the Active mode in FTP using `passive` command and use the `get` command to retrieve the remote-file `tbfc_qa_key1` and store it on the local machine.
    
    <aside>
    💡
    
    The issue is with **FTP passive mode** failing in THM OpenVPN setup (common due to VPN NAT/firewall restrictions on data ports). THM's AttackBox is a cloud VM with direct routing, so it works without issues—your Kali over OpenVPN gets stuck because the extended passive (EPSV) response can't establish the data connection for ls.
    ****
    
    </aside>
    
    ```bash
    $ cat tbfc_qa_key1
    KEY1:3aster_
    ```
    

---

What is the second key part found in the TBFC app?

> `15_th3_`
> 
- Moving on to the custom TBFC app on port `25251` , we don’t know what kind of service it is and how to access it, so we use netcat (`nc`), a universal tool to interact with network services:
    
    ```bash
    nc 10.80.156.231 25251
    help
    get key
    ```
    

---

What is the third key part found in the DNS records?

> `n3w_xm45`
> 
- To  check if the server is serving DNS:
    
    ```bash
    nc -sU -p53 10.80.156.231
    ```
    
- Now, we can use the `dig` tool to get more information about the DNS service
    
    ```bash
    dig @10.80.156.231 key3.tbfc.local TXT
    ```
    

---

Which port was the MySQL database running on?

> `3306`
> 
- Put the three keys together and use it to unlock the admin panel on the webpage
- On the web console, use the following command to see what internal services are running
    
    ```bash
    **tbfcapp@tbfc-devqa01:~$ ss -tulnp**                                                                                               
    Netid     State      Recv-Q     Send-Q              Local Address:Port          Peer Address:Port    Process                                                                                                                                          
    tcp       LISTEN     0          151                     127.0.0.1:3306               0.0.0.0:* 
    ```
    

---

Finally, what's the flag you found in the database?

> `THM{4ll_s3rvice5_d1sc0vered}`
> 
- Log into the local mysql service from the admin webpage with this command
    
    ```sql
    tbfcapp@tbfc-devqa01:~$ mysql
    ```
    
- Look through the database with these commands
    
    ```sql
    mysql> show databases;                                                      
    mysql> use tbfcqa01                                   
    mysql> show tables;                                         
    mysql> SELECT * FROM flags;            
    ```