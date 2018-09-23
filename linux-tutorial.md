<!-- TITLE: Linux Tutorial -->
<!-- SUBTITLE: A quick summary of Linux Tutorial -->

# Linux - tutorial
This is a step by step instruction of how to setup and run an elastic node on a dedicated server, or VPS including Ubuntu 16.04.

-----

**Preparing a Server for Client installation**

How to connect to your new server?

<p>If you are using Windows, download the latest <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html">Putty</a> Client and use these  instructions to connect to your server:</a> </p>

`https://mediatemple.net/community/products/dv/204404604/using-ssh-in-putty-`

If you are using Linux, start your console (Alt+Ctrl+T) and type:

`ssh username@youriporhostname.xyz`

 Once you are logged in you will start the installation of dependencies for your Elastic node to compile

`sudo apt update && sudo apt upgrade && sudo apt dist-upgrade`

(at this point, if you don’t have sudo installed and you are using a root account, just remove sudo from all the commands that will be shown in this tutorial)

 Install some basic packages
 
 `sudo apt install mc ntp fail2ban htop screen nano -y`
 
  Install Java

`sudo apt install software-properties-common -y
​
sudo add-apt-repository ppa:webupd8team/java
​
sudo apt update
​
sudo apt install oracle-java8-installer -y`



