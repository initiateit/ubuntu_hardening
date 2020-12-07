##  How to secure & harden your Ubuntu 20.04 installation

This is a simple guide to secure and harden your Ubuntu 20.04 server to make it not only as secure as it can be for vulnerabilites and potential attackers, but also performant.

#   Basics

## Update and Upgrade

Self explanatory.

    sudo apt update && sudo apt upgrade -y

##  Create a new user & add to sudo group

    adduser your_username_here && usermod -aG sudo your_username_here
    

##  Locking down access

We will want to remove the possibility of root being able to login and save us much of the hassle of problems that can occur from elevated permissions.

        sudo nano /etc/ssh/sshd_config

Change:

        PermitRootLogin no

Now restart the SSH server:

   sudo service ssh restart
