---
id: qsiuhzy3v7k05g8rcax8uqc
title: Linux
desc: ''
updated: 1717503517168
created: 1717503091941
---
sed - command for replacement inside a file.

In [[root.jenkins]] use \"{$var}\" for replacement to screen the quotes.

sudo netstat -tulpn | grep LISTEN  - display all open ports

ssh-keyscan -t rsa "10.53.228.101" - generate the known_hosts key entry for the rsa public key of the server.

ssh-keyscan -H 10.53.228.10 >> ~/.ssh/known_hosts  - adds the hostname/IP to the known_hosts, but only after pinging it
ssh-keygen -R "10.53.228.10" - removes the ssh key