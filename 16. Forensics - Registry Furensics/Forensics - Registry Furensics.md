# Forensics - Registry Furensics

- Open the Registry Explorer.
- Go to File > Load Hive.
- On the **Load hives** pop-up, navigate to `C:\Users\Administrator\Desktop\Registry Hives` .
- Select all the hives and **Hold SHIFT**, then press **Open** to load associated transaction log files. This ensures you get a clean, consistent hive state for analysis.
- You can use **Available Bookmarks** to search for the required values.

### Answer the questions below

What application was installed on the `dispatch-srv01` before the abnormal activity started?

> `DroneManager Updater`
> 

<aside>
💡

Search for `Uninstall` on Available bookmarks as it stores information on the installed programs.

</aside>

---

What is the full path where the user launched the application (found in question 1) from?

> `C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe`
> 

<aside>
💡

Search for `UserAssist`  on Available bookmarks as it stores information on recently accessed applications launched via the GUI.

</aside>

---

Which value was added by the application to maintain persistence on startup?

> `"C:\Program Files\DroneManager\dronehelper.exe" --background`
> 

<aside>
💡

 Search for `Run`on Available bookmarks as it stores information on the programs that are set to automatically start (startup programs) when the users logs in.

</aside>