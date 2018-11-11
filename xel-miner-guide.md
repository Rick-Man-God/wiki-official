<!-- TITLE: xel miner guide -->
<!-- SUBTITLE: xel miner guide -->

# About Xel Miner
-----

This tool is the core of the entire XEL network. Opposed to what the name suggests, it is way more than just a miner. It is a fully fledged ePL to C conversion and compilation tool, that helps you to convert your ePL program to C, compile it into executable machine code, and natively execute your ePL programs on your local machine. On top of that, it allows you to pull work from other scientists on the XEL network and search for solutions to their algorithms. Once a solution is found, xel_miner is capable of submitting it to the network in exchange for cryptocurrency rewards.

<div style="width:100%;height:0px;position:relative;padding-bottom:53.518%;"><iframe src="https://streamable.com/s/rh1ir/iotxek" frameborder="0" width="100%" height="100%" allowfullscreen style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe></div>

# Install Xel Miner
-----

The installation procedure is documented in the project README : https://github.com/xel-software/xel-miner#run-xel-miner-from-sources


# Using the Miner
-----

Once you are in the directory where your xel_miner executable is, its a good start to take a look at the help information xel_miner provides:

On linux and on macOS, that would be

```text
./xel_miner --help
```

On Windows


```text
xel_miner.exe --help
```

In the remainder of this tutorial, we will just cover the linux/macOS variant but the Windows one should be always analogous to that. After you have launched that command you will see the help:


```text
** XEL Compute Engine **
   Miner Version: 0.9.6
   ElasticPL Version: 0.9.4
Usage: xel_miner [OPTIONS]
Options:
  -c, --config          Use JSON-formated configuration file
      --deadswitch   Hardkill the instance after x seconds
  -D, --debug                 Display debug output
      --debug-epl             Display EPL source code
  -d, --delaysleep	     	  Sleep x seconds after submitting POW: useful for burstless debugging
   -i, --ignoremask			  Debug only: ignore 0=nothing, 1=PoW, 2=Bty, 3=Both
   -h, --help                 Display this help text and exit
  -m, --mining PREF[:ID]      Mining preference for choosing work
                                profit       (Default) Estimate most profitable based on POW Reward / WCET
                                wcet         Fewest cycles required by work item
                                workid		 Specify work ID
      --no-color              Don't display colored output
      --opencl	              Run VM using compiled OpenCL code
      --opencl-gthreads    Max Num of Global Threads (256 - 10240, default: 1024)
      --opencl-vwidth 	  Vector width of local work size (1 - 256, default: calculated)
  -o, --url=URL               URL of mining server
  -p, --pass        Password for mining server
  -P, --phrase    Secret Passphrase for XEL account
      --protocol              Display dump of protocol-level activities
  -q, --quiet                 Display minimal output
  -r, --retries            Number of times to retry if a network call fails
                              (Default: Retry indefinitely)
  -R, --retry-pause        Time to pause between retries (Default: 10 sec)
  -s, --scan-time          Max time to scan work before requesting new work (Default: 60 sec)
  	  --test-miner      Run the Miner using JSON formatted work in
      --test-vm         Run the Parser / Compiler using the XEL ePL source code in
	  --test-avoidcache   	  Do not save metadata
      --test-block 	  Block-id for test run
	  --test-cont-bounty      Search for bounties within test-vm environment
	  --test-cont-pow         Search for proof-of-work within test-vm environment
	  --test-work 	  Work-id for test run
	  --test-limit-storage 			Only allow storage sizes up to
	  --test-multiplicator <32-byte-hex>	Multiplicator for testrun: must be exactly 32 hex chars
	  --test-publickey <32-byte-hex>		Publickey for testrun: must be exactly 32 hex chars
	  --test-stdin		                    Read storage values from stdin
	  --test-target <16-byte-hex>		    Target for test run: must be exactly 16 hex chars
	  --test-wcet-main 		Do not ignore WCET limits of main function in Test-Vm run
	  --test-wcet-verify 	Do not ignore WCET limits of verify function in Test-Vm run
  -t, --threads            Number of miner threads (Default: Number of CPUs)
  -u, --user        Username for mining server
  -T, --timeout            Timeout for rpc calls (Default: 30 sec)
      --validate              Validate logic in 'main' & 'verify' functions
	  --verify-only           Use verify instead of main
  -v, --version               Display version information and exit
  -X  --no-renice             Do not lower the priority of miner threads
Options while mining ----------------------------------------------------------

   s +                 Display mining summary
   d +                 Toggle Debug mode
   q +                 Toggle Quite mode
```

We will not cover all options in this tutorial, only those which are required to get your miner ready to work on tasks on the XEL Blockchain. First of all, we want to take a look at the threads configuration parameter:


```text
-t, --threads            Number of miner threads (Default: Number of CPUs)
```

This parameter allows you to configure how many threads you want xel_miner to run on. The more threads you use, the faster xel_miner will find solutions. However, if you set this number too high your system may become unresponsive.

The next parameter we want to look at is the url configuration:


```text
-o, --url=URL               URL of mining server
```

This allows you to point the miner to either a remote node or a local node. Either way is fine, but keep in mind that remote URLs do leak your private key to the server at the moment. If you do not trust the remote node, stick to a local one instead. The URL is always given in the form of `http://hostname:port` where `hostname` is the IP or FQDN of the host, and `port` is either `17876` for the mainnet or `16876` for the testnet.

The third important parameter is the passphrase flag:


```text
-P, --phrase    Secret Passphrase for XEL account
```

`This is absolutely essential. `

This is the passphrase to the account which will both pay the transactions fees for submitting work results and receive the rewards in exchange. if your passphrase has a space in it, make sure to put double quotes around it.

`It is absolutely essential that you have some initial funds inside this account, otherwise you will not be able to submit any solutions. `

For testing purposes you can just use your 12 word Xeline mnemonic code (enclosed in double quotes) since it’s very easy to get some XEL from the faucet to get started.

Now, for this tutorial, we want to launch a miner running just one thread, mining via our local node on the testnet. Hence, we start it like this:


```text
./xel_miner -t 1 -o http://localhost:16876 -P "our twelve word passphrase goes here"
```

At this point, your miner is already solving proof-of-work packages and submitting bounties / solutions to algorithms for which it has found solutions. Let us take a look at one little anomaly here.

You have probably noticed these lines:


```text
[19:15:27] CPU0: ***** POW limit reached for this block, pausing until next block *****
[19:15:43] CPU0: ***** Bounty limit reached for this block, pausing until next block *****
```

The first line means that the maximum number of allowed POWs for this block has already been reached in the unconfirmed transaction cache and there is no need to submit more until the next block arrives. We already know, that the retargeting algorithm tries to calibrate the target value so that 10 proof-of-work submissions (on average) are found per minute. This is not per task but for all tasks in the network together. However, as a DOS precaution, there is a hard cap of 25 proof-of-work submissions per block. Once that number is reached, no more proof-of-work submissions are accepted until the next block is found.

The bounty limit behaves similarly. In this scenario we have a job that takes one bounty per iteration and runs for three iterations. Since one iteration corresponds to as least one full block, there is no need to submit more than one bounty per block. So once a bounty has been found (in this case, this can be more for other tasks), we have to wait until the iteration count increases by one in the next block.

`You do not need to continuously monitor the console output. If you launch Xeline, you can see a few basic mining statistics in the left sidebar`

Now, you are ready and set to start mining – be it your own tasks for testing purposes or other tasks for some XEL in exchange.

# Video tutorial
-----

## windows

[video](https://vimeo.com/265864726){.vimeo}


## macOS

<div style="width:100%;height:0px;position:relative;padding-bottom:78.148%;"><iframe src="https://streamable.com/s/0lsd6/tacmfb" frameborder="0" width="100%" height="100%" allowfullscreen style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe></div>


## linux

<div style="width:100%;height:0px;position:relative;padding-bottom:61.224%;"><iframe src="https://streamable.com/s/awnig/sdbuek" frameborder="0" width="100%" height="100%" allowfullscreen style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe></div>


