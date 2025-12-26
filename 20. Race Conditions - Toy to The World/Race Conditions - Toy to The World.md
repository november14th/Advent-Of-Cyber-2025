# Race Conditions - Toy to The World

**Steps:**

1. Visit  http://MACHINE_IP on browser.
2. Login: **`attacker:attacker@123`**
3. Burp Suite → Proxy → HTTP history → Find **`/process_checkout`** POST
4. Send to Repeater → Create tab group "cart" → Duplicate 15x
5. Repeater: "Send group in parallel (last-byte sync)"

**Result:** Multiple orders → Stock negative → Flag appears

**Targets:**

- SleighToy Limited Edition (10 stock)
- Bunny Plush (Blue)

**Fixes:** Atomic transactions, final stock check, idempotency keys, rate limiting

### Answer the questions below

What is the flag value once the stocks are negative for **SleighToy Limited Edition**?

> `THM{WINNER_OF_R@CE007}`
> 

Repeat the same steps as were done for ordering the SleighToy Limited Edition. What is the flag value once the stocks are negative for **Bunny Plush (Blue)**?

> `THM{WINNER_OF_Bunny_R@ce}`
>