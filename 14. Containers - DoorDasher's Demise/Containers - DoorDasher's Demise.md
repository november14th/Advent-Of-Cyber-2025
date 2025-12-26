# Containers - DoorDasher's Demise

### Answer the questions below

What exact command lists running Docker containers?

> `docker ps`
> 

---

What file is used to define the instructions for building a Docker image?

> `Dockerfile`
> 

<aside>
💡

Simple text script defining app environments and dependencies, to build, package, and run applications consistently across different systems.

</aside>

---

What's the flag?

> `THM{DOCKER_ESCAPE_SUCCESS}`
> 

<aside>
💡

On the CLI machine, use this command to interact with the `deployer` container `docker exec -it deployer bash`and there is a reset script in the top level directory, and we run this `/recovery_script.sh`. The file `flag.txt` is in `/` path where the `recovery_script.sh` resides.

</aside>

---

Bonus Question: There is a secret code contained within the news site running on port `5002`; this code also happens to be the password for the deployer user! They should definitely change their password. Can you find it?

> `DeployMaster2025!`
> 

<aside>
💡

Access the website `http://MACHINE_IP:5002` where there are three words highlighted red in the article on the webpage. Combine these together to get the password.

</aside>