---
layout: default
title: Set up OpenVPN and NodeJS on a server running Ubuntu 16.04
comments: true
---

## Find ssh public key.
```
// list all public keys.
ls ~/.ssh/*.pub

// copy public keyj
cat ~/.ssh/id_rsa.pub |pbcopy
```

## Copy SSH key to server
Use command `ssh-copy-id -i ~/.ssh/YOURKEY USERNAME@route.to.server` to copy the ssh to server, ask for password :)

Then use `ssh USERNAME@route.to.server` to connect to server.

## Set up firewall
Use UFW set up basic firewall. To list all applications that  has register their profiles:`sudo ufw app list`

Allows SSH connections: `sudo ufw allow OpenSSH`

Allow Specific IP Addresses: `sudo ufw allow from xx.xx.xx.xx`

Enable firewall: `sudo ufw enable`

Check status: `sudo ufw status`


## Set up OpenVPN on Ubuntu 16
Install OpenVPN.
```
sudo apt-get update
sudo apt-get install openvpn
```

Download .ovpn file
`curl -O https://config.ovpn`

Config & connect openVPN using .ovpn file

copy .ovpn file to `/etc/openvpn/` folder.
copy password file to `/etc/openvpn/` folder.
edit .openvpn file, add `auth-user-pass filename` in your .ovpn where filename is the file with username/password on 2 lines.

**Then rename the xxx.ovpn to xxx.conf file** for the deamon setup

 ```
	sudo systemctl start openvpn@client
	sudo systemctl status  openvpn@client
 ```


## Setup github
Install Git:
`sudo apt-get install git`

Checking for existing SSH keys:
`ls -al ~/.ssh`

If no SSH public key, generate new SSH key:
`ssh-keygen -t rsa -b 4096`

Add SSH key to the ssh-agent:
```
eval "$(ssh-agent -s)"  // run ssh-agent in background
ssh-add ~/.ssh/id_rsa   // add SSH Key
```
Add new SSH Key to Github account. https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-linux


## Install node.js
**DO NOT USE `sudo apt-get install nodejs`**
```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

## Allowed node.js access port 80
```
// Find node location
which node  // NODE_LOCATION/node
// Bind ports
setcap 'cap_net_bind_service=+ep' NODE_LOCATION/node
```

## Set up nodejs as ubuntu service, run nodejs as boot.
install forver:
`npm install forever -g`

Create and save the systemd service file in `/etc/systemd/system` as `myforever.service`.

https://www.axllent.org/docs/view/nodejs-service-with-systemd/
```
[Unit]
Description=Node.js Example Server
#Requires=After=mysql.service       # Requires the mysql service to run first

[Service]
ExecStart=/usr/local/bin/node /opt/nodeserver/server.js
# Required on some systems
#WorkingDirectory=/opt/nodeserver
Restart=always
 # Restart service after 10 seconds if node service crashes
 RestartSec=10
 # Output to syslog
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=nodejs-example
#User=<alternate user>
#Group=<alternate group>
Environment=NODE_ENV=production PORT=1337

[Install]
WantedBy=multi-user.target
```

```
systemctl start myforever.service
systemctl enable myforever.service
```

## References

Add user, set new user root privileges
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04

UFW document
https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-14-04

UFW common firewall rules and commands
https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands

Setup Github ssh connection
https://help.github.com/articles/checking-for-existing-ssh-keys/#platform-linux

Ubuntu install nodejs
https://github.com/nodesource/distributions

Get node instance
`ps -aux | grep node`

Running Node.js App With Systemd
https://nodesource.com/blog/running-your-node-js-app-with-systemd-part-1/

Set openvpn client conf file
https://help.ubuntu.com/lts/serverguide/openvpn.html