---
title: Install DOOM Eternal Mods in Linux
type: page
description: Secure SSH
topic: ssh
---

## Securing the OpenSSH server
- There are 2 important files for SSH configuration:
	- `/etc/ssh/ssh_config` file for the client
	- `/etc/ssh/sshd_config` file for SSH daemon

We will heavily focus on `sshd_config` to securing Linux server.
- Uncomment the a line by removing pound sign or hashtag to enable the option or parameter.

- Use a non standard port number for SSH connection listening in. This will avoid being seen by casual port scanner but not by targeted attacks. This is what we called security thorugh obscurity and this is not considered a good security practice in general because changing the port number does not make your server more secure.
`Port 2077`

- Disable direct root login. No matter how strong the root password is, there's always the possibility that the hacker can find the password using brute force attack. First make sure to create non-root user and create public key pair.
`PermitRootLogin no`

- Disable password authentication entirely if that's possible and enable only public key authentication. This is considered way more secure.
`PasswordAuthentication no`

- Configure ideal timeout interval. This means after pass a certain period of time that you set let say 300s, SSH daemon will send a message thorugh encrypted channel to request a response from the user. If still idle, user will be automatically logged out.
`ClientAliveInterval 300`
`ClientAliveCountMax 0`

### Optional
- Limit user's SSH access.
- Filter SSH access at the firewall level.
- Other parameter including:
    - `MaxAuthTries`
    - `MaxStartups`
    - `LoginGraceTime`
- You can check the rest of option in man page, `man sshd_config`
