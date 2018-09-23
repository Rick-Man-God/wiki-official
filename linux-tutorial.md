<!-- TITLE: Linux Tutorial -->
<!-- SUBTITLE: A quick summary of Linux Tutorial -->

# Linux - tutorial
This is a step by step instruction of how to setup and run an elastic node on a dedicated server, or VPS including Ubuntu 16.04.

-----

**Preparing a Server for Client installation**

How to connect to your new server?

<p>If you are using Windows, download the latest <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html">Putty</a> Client and use these  instructions to connect to your server:</a> </p>


```text
https://mediatemple.net/community/products/dv/204404604/using-ssh-in-putty-
```


If you are using Linux, start your console (Alt+Ctrl+T) and type:


```text
ssh username@youriporhostname.xyz
```


 Once you are logged in you will start the installation of dependencies for your Elastic node to compile


```text
sudo apt update && sudo apt upgrade && sudo apt dist-upgrade
```


(at this point, if you don’t have sudo installed and you are using a root account, just remove sudo from all the commands that will be shown in this tutorial)

 Install some basic packages
 
```text
sudo apt install mc ntp fail2ban htop screen nano -y
```

  Install Java

```text
sudo apt install software-properties-common -y

sudo add-apt-repository ppa:webupd8team/java

sudo apt update

sudo apt install oracle-java8-installer -y
```

(You’ll be prompt here to accept some TOS/License.)
After that, verify that your Java is installed in the right version

```text
java -version
```

 You should see something like this:


```text
Java version "1.8.0_121"

Java(TM) SE Runtime Environment (build 1.8.0_121-b13)

Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```

(Make sure Java is at 1.8.x because it’s currently supported by Elastic.)

-----

**Installing elastic client**

`Remember not to run Elastic as root user! `