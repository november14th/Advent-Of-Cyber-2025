# Passwords - A Cracking Christmas

# Walkthrough

- First we ssh into the target machine via our THM VPN connected machine.
    
    ```bash
    $ ssh ubuntu@10.82.177.162
    
    ubuntu@tryhackme:~$ 
    ```
    
- We navigate into the Desktop folder and look for file types (step 1).
    
    ```bash
    ubuntu@tryhackme:~/Desktop$ ls
    flag.pdf  flag.zip  john  mate-terminal.deskt
    ubuntu@tryhackme:~/Desktop$ file flag.*
    flag.pdf: PDF document, version 1.7, 1 page(s)
    flag.zip: Zip archive data, at least v2.0 to extract, compression method=AES Encrypted
    ```
    
- Now we pick tools based on file type (step 2)
    - PDF: `pdfcrack`, `john` (via `pdf2john`)
    - ZIP: `fcrackzip`, `john` (via `zip2john`)
    - General: `john` (very flexible) and `hashcat` (GPU acceleration, more advanced
- To crack the pdf using `pdfcrack`, we use the following command.
    
    ```bash
    ubuntu@tryhackme:~/Desktop$ pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt 
    found user-password: 'naughtylist'
    ```
    
- Since, we cannot crack zip files using `john`, we need to create a hash that John can understand.
    
    ```bash
    ubuntu@tryhackme:~/Desktop$ zip2john flag.zip > ziphash.txt 
    flag.zip/flag.txt:$zip2$*0*3*0*db58d2418c954f6d78aefc894faebf54*d89c*1d*b8370111f4d9eba3ca5ff6924f8c4ff8636055dce00daec2679f57bde1*57445596ac0bc2a29297*$/zip2$:flag.txt:flag.zip:flag.zip
    ```
    
- Now we can crack the `ziphash.txt` using `john` as follows:
    
    ```bash
    ubuntu@tryhackme:~/Desktop$ cat ziphash.txt 
    flag.zip/flag.txt:$zip2$*0*3*0*db58d2418c954f6d78aefc894faebf54*d89c*1d*b8370111f4d9eba3ca5ff6924f8c4ff8636055dce00daec2679f57bde1*57445596ac0bc2a29297*$/zip2$:flag.txt:flag.zip:flag.zip
    
    ubuntu@tryhackme:~/Desktop$ john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt
    
    winter4ever      (flag.zip/flag.txt) 
    ```
    
    ---
    
    ### Answer the questions below
    
    What is the flag inside the encrypted PDF?
    
    Either open the pdf via GUI or using `xdg-open` with pdf password: `naughtylist`
    
    > `THM{Cr4ck1ng_PDFs_1s_34$y}`
    > 
    
    What is the flag inside the encrypted zip file?
    
    You cannot unzip it with unzip but instead use `7z x flag.zip` with password: `winter4ever`
    
    > `THM{Cr4ck1n6_z1p$_1s_34$yyyy}`
    >