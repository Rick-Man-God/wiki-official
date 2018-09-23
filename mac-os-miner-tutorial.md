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
git clone https://github.com/xel-software/Miner-Mainnet
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
[video](https://vimeo.com/265864791){.vimeo}



 