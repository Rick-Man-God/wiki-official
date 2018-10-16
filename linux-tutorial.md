<!-- TITLE: Linux Tutorial -->
<!-- SUBTITLE: A quick summary of Linux Tutorial -->

# Linux - tutorial
This is a step by step instruction of how to setup and run an xel node on a dedicated server, or VPS including Ubuntu 16.04.

-----

**Preparing a Server for Client installation**
-----


How to connect to your new server?

<p>If you are using Windows, download the latest <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html">Putty</a> Client and use these  instructions to connect to your server:</a> </p>


```text
https://mediatemple.net/community/products/dv/204404604/using-ssh-in-putty-
```


If you are using Linux, start your console (Alt+Ctrl+T) and type:


```text
ssh username@youriporhostname.xyz
```


 Once you are logged in you will start the installation of dependencies for your XEL node to compile


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

(Make sure Java is at 1.8.x because it’s currently supported by XEL.)

-----

**Installing XEL client**
-----


`Remember not to run XEL as root user! `

If at this point you are logged in as root user, create a new account and do the rest of the command with this new user. You can skip this step if you have access to a normal user.


```text
adduser xel
```

You’ll be asked some questions about the user. Just drop some data. Then set a password for the new user. Remember that the password needs to be strong (min 16 chars, min one upper case letter, min one lower case letter, min one number). Use a password generator if you don’t want to burn your brain, but remember to keep that password in some safe place.


```text
passwd xel
```

Logout from root account. We don’t need it anymore.

`Remember not to login to root account anymore!`

If by accident you’ll login to your root account and run for example XEL from it, some file permission will change and you’ll not be able to run XEL with this newly created user anymore.


```text
exit
```

Login as xel this time typing your newly created password. You should be in your home directory now. Check it by typing


```text
pwd
```

You should see



```text
/home/exel
```

Launch MC and hit F7 to create a new directory. Name it ‘xel’ as well (without quotes of course). Go to this directory and minimize MC (Ctrl + O).

Paste/type


```text
git clone https://github.com/xel-software/xel-lite-wallet.git
```

Maximize MC (Ctrl + O) and go to the xel-lite-wallet directory. Minimize and


```text
./compile.sh
```

Maximize, and this time you have to exit MC (F10). You need to go to the xel-lite-wallet directory manually because you will need to launch it in screen. So if you have directory structure like mentioned before, you can type:


```text
cd /home/xel/xel/xel-lite-wallet
```

And you should be in xel-lite-wallet directory. If your username is different (i.e ubuntu) type:


```text
cd /home/ubuntu/xel/xel-lite-wallet
```


Hope you get the idea. If you for some reason lost, read about ‘ls’ command it will help navigate listing files and directories in directory you currently are.

If you’re in xel-lite-wallet directory type


```text
screen ./run.sh
```

What this command do it’ll pull latest changes from github, compile it with maven and launch XEL. Check if everything launch as it should.

If you want to go back from screen to your server console` **LEAVING XEL running in background** `hit Ctrl (hold it), now hit A key` **and release it** `and hit D key.

You should be back in console and XEL is running in background so if you exit your server XEL will be still running.
If you want to go back to XEL (for example to shutdown it) type


```text
screen -r
```

This command should bring your screen instance of xel (even if you login to your node next time)
If you want to shutdown xel hit Ctrl + C. xel and screen itself should exit.

Now (once XEL is down) i.e. you can update XEL to the newest version and launch it again


```text
cd /home/xel/xel/xel-lite-wallet

git pull

./compile.sh

screen ./run.sh
```

At this point you have full relay node up and runnig! You are already helping the network, you don’t need to know anything more if you just wanted to help with relay blocks/txs. Just remember to update your node when a new version will show up.

But you might also want to login to your wallet with the browser to start forging for example (or just see if it work as it should, see blocks, txs etc).
You’ll also need to create an SSL cert to protect yourself against Main-In-The-Middle attack.

First, you need to stop your XEL node (see above) and do some config change in order to be able to access it remotely.

Next, we need to generate an SSL certificate


```text
cd /home/xel/xel/xel-lite-wallet
```
-----
```text
keytool -genkeypair -keyalg RSA -keysize 2048 -validity 3650 -keystore keystore
```

You’ll be asked here for some basic info about your certificate (fill it all with XEL word) AND for passphrase. Remember to set here some strong password (min 32 random chars, best use password generator), paste here and keep it safe. You’ll need that password in a minute.
Launch mc and go to your XEL-Litewallet/conf directory. When you’re in conf directory minimize MC (Ctrl + O) Type


```text
touch nxt.properties
```

This will be the file where you customize any default properties xel has. If you want to see all of that properties there are in nxt-default.properties file. You can go to this directory with mc, mark that file and hit F4 to see it contents (you’ll be asked here to choose default editor, nano is quite easy). When you stop reading and want to exit nano hit Ctrl + X (and hit N to not save any changes). Remember, you can’t change content of nxt-default.properties because everything you’ll change there will be overwritten next time you’ll update your xel. Thats why we created a new file in conf directory.
So, go back to conf/nxt.properties, highlight that file in MC, and edit it (F4). You’ll see an empty file. Paste the following lines there:


```text
# Hosts from which to allow http/json API requests, if enabled. Set to * to
​
# allow all. Can also specify networks in CIDR notation, e.g. 192.168.1.0/24.
​
nxt.allowedBotHosts=*
​
# Host interface on which to listen for http/json API request, default localhost
​
# only. Set to 0.0.0.0 to allow the API server to accept requests from all
​
# network interfaces, including IPv6.
​
nxt.apiServerHost=0.0.0.0
​
# Password that should be provided when executing protected (administrative) API
​
# requests.
​
# Please choose a decent password here. Preferably, use a password generator.
​
# Password protection is disabled and password is not needed when the API server
​
# only listens on the localhost interface, i.e. when
​
# nxt.apiServerHost=127.0.0.1.
​
nxt.adminPassword=generateSomeAdminAPIPasswordAndPasteHere
​
# Enable SSL for the API server (also need to set nxt.keyStorePath and
​
# nxt.keyStorePassword).
​
# Non-SSL connections will be disabled if nxt.apiServerSSLPort is equal to
​
# nxt.apiServerPort.
​
# Otherwise, both SSL and non-SSL connections will be accepted.
​
nxt.apiSSL=true
​
# keystore file and password, required if uiSSL or apiSSL are enabled.
​
nxt.keyStorePath=keystore
​
nxt.keyStorePassword=passwordYouProvidedDuringSSLCertGeneration
```

As you can see, adminPassword is “generateSomeAdminAPIPasswordAndPasteHere”. Again, generate yet another password here. You don’t need to save this password anywhere because you don’t need it. It just has to be set when you are opening your node to the world.

keyStorePassword is “passwordYouProvidedDuringSSLCertGeneration”. Replace it with password you generated during the SSL step.

Save your changes by hitting Ctrl + X (you’ll be asked if you want to save, hit Y or if you have Ubuntu installed in different language, it might be a key corresponding to “Yes” word in your language) and you should be back in MC. Exit from mc (F10):


**Running the node**
-----


```text
cd /home/xel/xel/xel-lite-wallet
```


```text
screen ./run.sh
```

If you want to go back from screen to your server console` **LEAVING XEL running in background** `hit Ctrl (hold it), now hit A key` **and release it** `and hit D key.

To access ur wallet open ur browser and go to


```text
https://your_server_ip_address_or_hostname:17876
```
