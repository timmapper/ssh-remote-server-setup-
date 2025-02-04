# SSH Remote Server Setup
Roadmap.sh project link: https://roadmap.sh/projects/ssh-remote-server-setup

## Setting Up
1. Create a server
   
   Use any provider to create a VPS. After purchasing you will receive an email with IP, user and password. These info need to connect the server.

    ```ssh <user>@<IPv4 address>```
2. Setup SSH connection
  
    First of all, you need to update packages.

    ```sudo apt update && apt upgrade -y```

   After this, generate a ssh key pair on your local machine

   ```ssh-keygen -t rsa -b 4096```

   If you will be asked for the file path, use ~/.ssh/"filename"
   There will be created two files: "filename" (private key) and "filename".pub (public key)

   Now copy the public key to the server

   ```ssh-copy-id -i ~/.ssh/<filename>.pub <user>@<IPv4 address>```

   You can make sure that public key has been copied to the server. Check server's .ssh/authorized_keys to check with Nano. If there is no key, just copy the public key in this file.

   The next step is the turning off password authentification. Open /etc/ssh/sshd_config with nano and find this string:

   ```PasswordAuthentication yes```

   Replace 'yes' to 'no'

3. Configure local SSH Access

   Create ~/.ssh/config file to set alias for connecting to the server and write:

   ```
    Host <aliasfortheserver>
    	HostName <IPv4address>
    	User <user>
    	IdentityFile ~/.ssh/<filename>
    	Port <port> #by default, 22
    	IdentitiesOnly yes
   ```

   Now you can use ```ssh <aliasfortheserver>``` to connect
