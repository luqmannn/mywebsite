---
title: Everything About OpenSSH

date: 2023-03-05
type: page
categories:
    - Linux
tags:
    - SSH 
    - Bash
---

### Introduction
If you work as a system administrator or generally in IT, it is pretty common to use OpenSSH to login into remote machine or server. By default, most Linux distribution came pre-installed with it. OpenSSH use SSH protocol to establish secure remote connection to the other machine through port 22 which you can change later in the config file. Below are some of the things I consider important to know and how to use it, also some of the tips and trick. [More detail about secure SSH](https://stribika.github.io/2015/01/04/secure-secure-shell.html)

### Basics
The component that responsible for receiving remote connection to the server is `sshd` which is the short form of _SSH daemon_. To check if the SSH daemon is enable or not.
```{sh}
systemctl status sshd
```

If not enable, enable SSH daemon right now.
```{sh}
sudo systemctl enable --now sshd
```

SSH keys provides greater security and at the same time allow convenience for the user to connect to the remote machine. To generate an **ED25519** SSH key pair (public and private key).
```{sh}
ssh-keygen -t ed25519 -C "anycomment"
``` 
- [GitLab recommendation on why use ED25519](https://docs.gitlab.com/ee/user/ssh.html#ed25519-ssh-keys)
- The comment earlier will be append at the end of public key. If there is no comment, it’ll back to default `username@thenameofcomputer`. 
- Consider naming the keys in a way that make logical sense such as the server name according to the client or server purpose.
> It is highly recommended to enter the passphrase for the keys, especially when working with the clients.

Copying public key can be done manually. `cat id_ed25519.pub` file directly and copy public key inside the file straight into the `authorized_keys` file in the `.ssh` directory on the remote machine. If there is none of the file, create one. But, this process can be done easily using `ssh-copy-id`. To copy public key to the remote machine (server). 
```{sh}
ssh-copy-id -i ~/.ssh/id_ed25519.pub username@ip_address
```
- It will automatically create `.ssh/authorized_keys` file if there is none.

To connect to the remote machine using specific private key.
```{sh}
ssh -i ~/.ssh/id_ed25519 username@ip_address
```

To connect to the remote machine as usual, if there is only one key.
```{sh}
ssh username@ip_address
```

To view more information about the connection, use `-v` flag.
```{sh}
ssh -v username@ip_address
```
- **Ctrl + D** to disconnect from the remote machine.

### Manage OpenSSH client
Create an empty file name `config` in `.ssh` directory and edit the file using any text editor. Then put the detail as shown like the format down below:
```{bash}
Host customer1
     Hostname 192.168.1.12
     Port 22
     IdentityFile ~/.ssh/id_ed25519
     User archie
```

Config parameter | Description
---------------- | ------------
Host             | The prefer name use to initiate SSH connection.
Hostname         | Remote machine (server) IP address
Port             | Port number of SSH remote machine, default is 22
IdentityFile     | Point to private key, such as ED25519
User             | Username of remote machine.

Save the file and exit. This is to simplify the process of connecting to the remote machine, so no need to enter IP address every time user want to connect. User can include multiple or any number of remote server that they want in this file. Use this format `ssh customer1` instead of `ssh username@ip_address` which is far shorter and less time to type. It is easy for user and they can include any server they want and label it with any name scheme as they wish.

It is common to have few of SSH keys in the `.ssh` folder when managing multiple server or remote machine. This is because user need to generate SSH keys specific to that server to differentiate the keys from the other. Having a separate key for each server is a good idea but it had to be **managed carefully**, if not SSH possibly will try different key multiple times resulting user get locked out of the server.

### Configure OpenSSH server
Edit the file to configure OpenSSH server.
```{sh}
nano /etc/ssh/sshd_config
```

In this file, user can edit the file by uncomment a line to enable and change the value as it fit the use case. For example port number can be changed to the other port number, as long as it doesn’t occupied the port currently in use such as port 80 for web server. 
```
Port 22
PermitRootLogin yes
PasswordAuthentication yes
```

Become:
```
Port 2222
PermitRootLogin no
PasswordAuthentication no
```
> For **PermitRootLogin**, it can be changed to no but make sure to **set up non-root user** beforehand with SSH enabled. Because if fail to do so, user **wouldn’t be able** to connect to the remote machine permanently. 

> For the **PasswordAuthentication** option, it can be changed to no if user already set up SSH keys and **make sure** that SSH keys can be used to login to the remote machine.

Make sure to restart SSH service after the changes.
```{sh}
sudo systemctl restart sshd
```