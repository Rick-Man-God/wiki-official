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

If at this point you are logged in as root user, create a new account and do the rest of the command with this new user. You can skip this step if you have access to a normal user.


```text
adduser elastic
```

You’ll be asked some questions about the user. Just drop some data. Then set a password for the new user. Remember that the password needs to be strong (min 16 chars, min one upper case letter, min one lower case letter, min one number). Use a password generator if you don’t want to burn your brain, but remember to keep that password in some safe place.


```text
passwd elastic
```

Logout from root account. We don’t need it anymore. 

`Remember not to login to root account anymore!`

If by accident you’ll login to your root account and run for example Elastic from it, some file permission will change and you’ll not be able to run Elastic with this newly created user anymore.


```text
exit
```

Login as elastic this time typing your newly created password. You should be in your home directory now. Check it by typing


```text
pwd
```

You should see



```text
/home/elastic
```

Launch MC and hit F7 to create a new directory. Name it ‘elastic’ as well (without quotes of course). Go to this directory and minimize MC (Ctrl + O).

Paste/type


```text
git clone https://github.com/xel-software/Litewallet-Mainnet.git 
```

Maximize MC (Ctrl + O) and go to the Litewallet-Mainnet directory. Minimize and


```text
./compile.sh
```

Maximize, and this time you have to exit MC (F10). You need to go to the Litewallet-Mainnet directory manually because you will need to launch it in screen. So if you have directory structure like mentioned before, you can type:


```text
cd /home/elastic/elastic/Litewallet-Mainnet
```

And you should be in Litewallet-Mainnet directory. If your username is different (i.e ubuntu) type:


```text
cd /home/ubuntu/elastic/Litewallet-Mainnet
```


Hope you get the idea. If you for some reason lost, read about ‘ls’ command it will help navigate listing files and directories in directory you currently are.

If you’re in Litewallet-Mainnet directory type


```text
screen ./run.sh
```

What this command do it’ll pull latest changes from github, compile it with maven and launch Elastic. Check if everything launch as it should.

`If you want to go back from screen to your server console` **LEAVING Elastic running in background** `hit Ctrl (hold it), now hit A key` **and release it** `and hit D key.` 

You should be back in console and Elastic is running in background so if you exit your server Elastic will be still running.
If you want to go back to Elastic (for example to shutdown it) type


```text
screen -r
```

This command should bring your screen instance of elastic (even if you login to your node next time)
If you want to shutdown elastic hit Ctrl + C. elastic and screen itself should exit.

Now (once Elastic is down) i.e. you can update Elastic to the newest version and launch it again


```text
cd /home/elastic/elastic/Litewallet-Mainnet

git pull

./compile.sh

screen ./run.sh
```
