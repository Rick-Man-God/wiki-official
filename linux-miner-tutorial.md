<!-- TITLE: Linux Miner Tutorial -->
<!-- SUBTITLE: A quick summary of Linux Miner Tutorial -->

# Linux - miner tutorial
Install from Source
-----


```text
# Make sure you have all dependencies installed
sudo apt-get install git libgmp-dev libcurl4-openssl-dev libssl-dev build-essential cmake
​
# Get the latest source code (or run a git pull to update)
git clone https://github.com/xel-software/xel-miner
​
# Run CMake inside xel_miner folder
cd xel_miner
cmake .
​
# Compile
make
```

You can test if it’s functioning properly by running:


```text
sudo ./xel_miner --test-vm examples/SHA256_BTC.epl
```

Use this exemple for mining


```text
sudo ./xel_miner -t 1 -o http://nodeip:17876 -P "12 words your passphrase"
```


`-t 1` stand for cpu threads `-o` Node address with port `-P` 12 words your passphrase

 Video tutorial
-----
<div style="width:100%;height:0px;position:relative;padding-bottom:61.224%;"><iframe src="https://streamable.com/s/awnig/sdbuek" frameborder="0" width="100%" height="100%" allowfullscreen style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe></div>
