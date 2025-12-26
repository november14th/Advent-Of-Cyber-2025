# IDOR - Santa’s Little IDOR

# Walkthrough

1. Navigate to the web browser and go to the site `http://10.81.175.124` and login with `niels: TryHackMe#2025`
2. DevTools → Network → view_accountinfo → user_id=10 (own account)
3. Storage → Local Storage → auth_user → Change user_id=11 → Refresh → IDOR works
4. Iterate user_id values → Find parent with 10 children
5. Child eye icon → Base64 "Mg=="=2 → Decode/iterate other IDs
6. Edit icon → MD5 hash → Hash identifier tool → Replicate for brute force
7. Vouchers → UUIDv1 decoder → Generate timestamps 2025-11-20 20:00-24:00 UTC

### Answer the questions below

What does IDOR stand for?

> `Insecure Direct Object Reference`
> 

---

What type of privilege escalation are most IDOR cases?

> `Horizontal`
> 

---

Exploiting the IDOR found in the `view_accounts` parameter, what is the `user_id` of the parent that has 10 children?

<aside>
💡

Iterate view_accountinfo user_id=10,11,12... until finding parent with 10 children

</aside>