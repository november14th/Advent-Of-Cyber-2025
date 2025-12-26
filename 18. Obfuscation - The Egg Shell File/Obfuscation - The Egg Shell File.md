# Obfuscation - The Egg Shell File

- Open **SantaStealer.ps1**, located on the VM's Desktop in Visual Studio by double clicking it (takes a moment to open), and navigate to the "**Start here**" section of the script
- Follow the instructions in the code's comments and save, then run the script from a PowerShell terminal.
    
    ```jsx
    PS C:\Users\Administrator> cd .\Desktop\
    PS C:\Users\Administrator\Desktop> .\SantaStealer.ps1
    ```
    

### Answer the questions below

What is the first flag you get after deobfuscating the C2 URL and running the script?

> `THM{C2_De0bfuscation_29838}`
> 

<aside>
💡

- Deobfuscate the string “`aHR0cHM6Ly9jMi5ub3J0aHBvbGUudGhtL2V4Zmls`” `From Base64` present in the `$C2B64` variable.
- Place the URL “`https://c2.northpole.thm/exfil`” in `$C2` variable.
- Run the script.
</aside>

---

What is the second flag you get after obfuscating the API key and running the script again?

> `THM{API_Obfusc4tion_ftw_0283}`
> 

<aside>
💡

- Obfuscate the API key `"CANDY-CANE-API-KEY”` using XOR single-byte key `0x37` and convert to `hexidecimal` using Cyberchef recipe `XOR(”key”: 0x37)` →`To Hex`.
- Add the hex string “`747679736e1a747679721a76677e1a7c726e` ” to the `$ObfAPieEy` variable.
    
    ```jsx
    $ObfAPIKEY = Invoke-XorDecode -Hex "747679736e1a747679721a76677e1a7c726e" -Key 0x37
    ```
    

</aside>