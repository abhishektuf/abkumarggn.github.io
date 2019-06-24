---
layout: post
title: "ssh authentication based on public keys"
date: 2013-11-19
---

we can use public key based authentication to logon to ssh session on any linux / unix server. In this method logons are performed passwordless and more secure as it involves rsa keys which are 2048 bit or more in length


steps for setup a secure logon using SSH

1. generate one key pair (one public + one private) using puttygen utility (recommended key length is more than 2048 bit RSA)


2. copy paste the public from puttygen window to ~/.ssh/authorized_keys file on destination server

3. chmod 600 ~/.ssh/authorized_keys file on the server or you will get “Authentication refused: bad ownership or modes for file /home/user/.ssh/authorized_keys”

4. chmod 655 ~/.ssh (directory) or else you will get “Authentication refused: bad ownership or modes for directory /home/user/.ssh” in secure log

5. provide the username in connection >> data on putty screen


6. select save private key from the puttygen window to somewhere on your windows pc


7. now select this key while opening a session in putty (go to connection >> SSH >> Auth ) screen window


8. now your session should be up and running without any further prompts

one more point to note down is DSA keys are used only in SSHv1 whereas RSA is latest and secure and used by default in SSHv2 , also recommended.
