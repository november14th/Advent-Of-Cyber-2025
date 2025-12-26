# C2 Detection - Command & Carol

```bash
## Convert PCAP to Zeek logs
ubuntu@tryhackme$ zeek readpcap pcaps/rita_challenge.pcap zeek_logs/rita_challenge

## Analyze logs, create database
ubuntu@tryhackme$ rita import --logs ~/zeek_logs/rita_challenge/ --database rita_challenge  

## View the result
ubuntu@tryhackme$ rita view rita_challenge
```

<aside>
💡

- To search, we need to enter a forward slash (`/`).
- When we enter `?` while in search mode, we can see an overview of the search fields, alongside some examples.
- To exit the help page, enter `?` again.
- Enter the escape key ("esc") to exit the search functionality.
</aside>

### Answer the questions below

How many hosts are communicating with **malhare.net**?

> `6`
> 

<aside>
💡

Answer from Prevalence column

</aside>

---

Which Threat Modifier tells us the number of hosts communicating to a certain destination?

> `prevalence`
> 

---

What is the highest number of connections to **rabbithole.malhare.net**?

> `40`
> 

<aside>
💡

Answer from Connection count in details pane

</aside>

---

Which search filter would you use to search for all entries that communicate to **rabbithole.malhare.net** with a **beacon score** greater than 70% and sorted by **connection duration (descending)**?

> `/dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc`
> 

Which port did the host 10.0.0.13 use to connect to **rabbithole.malhare.net**?

> `80`
> 

<aside>
💡

Select 10.0.0.13 entry → Details pane → Port info

</aside>