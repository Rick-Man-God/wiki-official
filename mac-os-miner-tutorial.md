<!-- TITLE: Mac Os Miner Tutorial -->
<!-- SUBTITLE: A quick summary of Mac Os Miner Tutorial -->

# MacOS - miner tutorial
Install from Source
-----


```text
# Make sure you have homebrew installed (if you do, skip this step):
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
​
# Make sure to install all required dependencies
brew install gmp make cmake openssl
​
# Get the latest source code (or run a git pull to update)
git clone https://github.com/xel-software/xel-miner
​
# Make sure to link the OpenSSL include directory to the right place
ln -s /usr/local/opt/openssl/include/openssl/ /usr/local/include/openssl
​
# Compile the miner
cd xel_miner
OPENSSL_ROOT_DIR=/usr/local/opt/openssl cmake .
make
```

You can test if it’s functioning properly by running:


```text
xel_miner --test-vm examples/SHA256_BTC.epl
```

se this exemple for mining 


```text
xel_miner -t 1 -o http://nodeip:17876 -P "12 words your passphrase"
```


`-t 1` stand for cpu threads `-o` Node address with port `-P` 12 words your passphrase

Video tutorial
-----
<div style="width:100%;height:0px;position:relative;padding-bottom:78.148%;"><iframe src="https://streamable.com/s/0lsd6/tacmfb" frameborder="0" width="100%" height="100%" allowfullscreen style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe></div>



 