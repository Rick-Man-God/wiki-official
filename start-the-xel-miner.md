<!-- TITLE: Start The Xel Miner -->
<!-- SUBTITLE: A quick summary of Start The Xel Miner -->

# Start the xel miner
-----
In this tutorial, we want to demonstrate how to use the miner to actually work on tasks on the XEL blockchain. We will not go through every tiny little function of the miner (this is something for a future article), yet we will cover everything you need to know to get started mining.

-----

Prerequisites (optional)
-----
Before you get started, you have to decide whether you want to use the miner remotely, or if you want to mine through a local node. In the case of Xeline, it is absolutely fine to use a remote wallet, since the signing is done locally, and your private key never leaves your computer. This is different in the case of the miner: when submitting proof-of-work results or solution candidates, your private key is submitted to the server as well, since the miner, as of now, has no logic to sign transactions built in. We hope that this will change in the future.

So the safest bet is to set up a local XEL node on your system. Before you do so, you have to make sure that you have a working Docker installation and that docker is fully functional on your computer. There are thousands of guides on how to do it for all different kinds of platforms.

In a next step, you have to clone the XEL docker repository

```text
git clone https://github.com/xel-software/Computationwallet-Mainnet-Docker.git
```

Now, go into the `xel_docker directory` and launch

```text
docker build -t xel .
```

If something goes wrong, you probably do not have the docker executable in your PATH – you might want to double check this. After a few minutes of waiting, your XEL docker image should be ready. If you are on a linux of macOS machine, launching the node is fairly simple. Just use the following bash script:

```text
./run_with_computation.sh
```

If you are on Windows, launch it by using Docker directly instead. Make sure you launch this command from within the xel-docker/ directory.

```text
docker run -p 17876:17876 -p 17874:17874 -p 16876:16876 -p 16874:16874 --mount type=bind,source=xel_data_dir,target=/elastic-core-maven/nxt_test_db --mount type=bind,source=conf,target=/elastic-core-maven/conf_user -i -t xel
```

Now, you have to give the node some time. You want it to synchronize the blockchain entirely before you proceed. Maybe it’s time for an extended walk, a coffee or just a short break.

-----
Installing the Miner
-----
The installation of the miner is `covered in our article on how to become a master at ePL.` If you haven’t done so, please follow the installation instructions over there.

-----

Using the Miner
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
** Elastic Compute Engine **
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
  -P, --phrase    Secret Passphrase for Elastic account
      --protocol              Display dump of protocol-level activities
  -q, --quiet                 Display minimal output
  -r, --retries            Number of times to retry if a network call fails
                              (Default: Retry indefinitely)
  -R, --retry-pause        Time to pause between retries (Default: 10 sec)
  -s, --scan-time          Max time to scan work before requesting new work (Default: 60 sec)
  	  --test-miner      Run the Miner using JSON formatted work in 
      --test-vm         Run the Parser / Compiler using the ElasticPL source code in 
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

