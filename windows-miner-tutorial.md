<!-- TITLE: Windows Miner Tutorial -->
<!-- SUBTITLE: A quick summary of Windows Miner Tutorial -->

# Windows - miner tutorial
-----

Install from binary
-----
```text
# Download the latest (experimental CPU only) binary version from:
https://github.com/xel-software/xel-miner/releases
```

After you unzip the archive, go into the folder `xel_miner-0.9.6/xel_miner`. There, you will find the `xel_miner.exe` executable. You can test if it’s functioning properly by running:


```text
xel_miner.exe --test-vm examples\SHA256_BTC.epl
```

If you encounter any errors, the reason may be that you already have a MinGW installation on your system and in your `PATH`. In this case, try to clean the `PATH` variable by doing a simple


```text
set PATH=
```

To start mining use `CMD` go to directory of miner

```text
cd c:/xel_miner-0.9.6/xel_miner
```

Use this exemple for mining


```text
xel_miner.exe -t 1 -o http://nodeip:17876 -P "12 words your passphrase"
```


`-t 1` stand for cpu threads `-o` Node address with port `-P` 12 words your passphrase

Video tutorial
-----

[video](https://vimeo.com/265864726){.vimeo}
