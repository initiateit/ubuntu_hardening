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

        AllowUsers your_username_here

### Even better if you have a static IP then lock down your account to one address

You can either define your IP address or a range. For example 123.123.123.123 or 10.88.88.0/24 IP addresses only, wjile yurisk will be able to connect from anywhere.

        AllowUsers your_username_here@111.10.1.1           #Will only allow SSH connections from 111.10.1.1
        AllowUsers your_username_here@111.10.1.*           #Will only allow SSH connections from 111.10.1.0/24 Range
