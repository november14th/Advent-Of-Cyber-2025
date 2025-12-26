# YARA Rules - YARA mean one!

# Walkthrough

### Answer the questions below

How many images contain the string TBFC?

> `5`
> 

```yaml
rule TBFC_String
{
	meta:
		description: "Count the string TBFC"
	strings:
		$my_text_string = "TBFC"
	condition:
		$my_text_string
}
```

```bash
ubuntu@tryhackme:~/Downloads/easter$ yara test.yar .
TBFC_String ./test.yar
TBFC_String ./easter46.jpg
TBFC_String ./embeds
TBFC_String ./easter10.jpg
TBFC_String ./easter16.jpg
TBFC_String ./easter52.jpg
TBFC_String ./easter25.jpg
```

---

What regex would you use to match a string that begins with `TBFC:` followed by one or more alphanumeric ASCII characters?

> `/TBFC:[A-Za-z0-9]+/`
> 

---

What is the message sent by McSkidy?

> `Find me in HopSec Island`
> 

```bash
rule Message
{
	meta:
		description: "Message sent by McSkidy"
	strings:
		$my_text_string = /TBFC:[A-Za-z0-9]+/ ascii
	condition:
		$my_text_string
}
```

```bash
ubuntu@tryhackme:~/Downloads/easter$ yara -s message.yar .
TBFC_String ./easter46.jpg
0x2f78a:$my_text_string: TBFC:HopSec
TBFC_String ./easter10.jpg
0x137da8:$my_text_string: TBFC:Find
TBFC_String ./easter16.jpg
0x3bb7f7:$my_text_string: TBFC:me
TBFC_String ./easter25.jpg
0x42c778:$my_text_string: TBFC:in
TBFC_String ./easter52.jpg
0x2a2ad2:$my_text_string: TBFC:Island
```

Arranging it in ascending order, we get `Find me in HopSec Island`