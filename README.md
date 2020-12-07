##  How to secure & harden your Ubuntu 20.04 installation

This is a simple guide to secure and harden your Ubuntu 20.04 server to make it not only as secure as it can be for vulnerabilites and potential attackers, but also performant.

#   Basics

## Update and Upgrade

Make sure we are up to date with both packages available and packages installed.

    sudo apt update && sudo apt upgrade -y

##  Create a new user & add to sudo group

    adduser your_username_here && usermod -aG sudo your_username_here
    

##  Locking down access

We will want to remove the possibility of root being able to login and save us much of the hassle of problems that can occur from elevated permissions.

        sudo nano /etc/ssh/sshd_config

Change <code>PermitRootLogin</code> to:

        PermitRootLogin no

Now restart the SSH server:

        sudo service ssh restart

##  Lock down access to SSH to a single user or multiple users

        sudo nano /etc/ssh/sshd_config

Add to the bottom of the file;

        DenyUsers all
        AllowUsers your_username_here

### Even better if you have a static IP then lock down your account to one address

You can either define your IP address or a range. For example 111.10.1.1 or 111.10.1.*

        AllowUsers your_username_here@111.10.1.1           #Will only allow SSH connections from 111.10.1.1
        AllowUsers your_username_here@111.10.1.*           #Will only allow SSH connections from 111.10.1.0/24 Range

## Change the default SSHD port

Yes those invested enogh with port scanners will have no issue finding your port, but port obfuscation shouldnt be seen as an independant layer of security. Its just another level of weeding out attacks from less "invested" attackers. You will rid yourself of many bot attacks and when used in conjunction with other measures it all adds up. Specify a  port below 1024 to prevent unprivelaged processes from binding to it and impersonating it. For a list of ports and what they do check here: 
https://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-sg-en-4/ch-ports.html

Edit:

        sudo nano /etc/ssh/sshd_config

Change:

        Port <port under 1024>
