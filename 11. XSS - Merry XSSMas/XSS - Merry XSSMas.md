# XSS - Merry XSSMas

# Walkthrough

### Answer the questions below

Which type of XSS attack requires payloads to be persisted on the backend?

> `stored`
> 

What's the reflected XSS flag?

> `THM{Evil_Bunny}`
> 

<aside>
💡

Inject the code `<script>alert('Reflected Meow Meow')</script>` by adding the payload to the search bar and clicking " **Search Messages**"

</aside>

![System log](XSS%20-%20Merry%20XSSMas/image.png)

System log

---

What's the stored XSS flag?

> `THM{Evil_Stored_Egg}`
> 

<aside>
💡

Navigate to the message form, and enter the malicious payload `<script>alert('Stored Meow Meow')</script>` . Click the " **Send Message**" button. Because messages are stored on the server, every time you navigate to the site or reload, the alert will display

</aside>

![System log](XSS%20-%20Merry%20XSSMas/image%201.png)

System log