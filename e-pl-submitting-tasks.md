<!-- TITLE: E Pl Submitting Tasks -->
<!-- SUBTITLE: A quick summary of E Pl Submitting Tasks -->

# ePL – Submitting Tasks
-----

It Is Time to Submit Your Task to the Blockchain. Before you do so, we strongly recommend that you read and understand the guide found here. We will be reusing this example in this guide. The difference is, while we were testing the code just locally in the previous guide, we will submit that task to the XEL Blockchain.

-----
Getting Xeline Ready
-----
This tool comes in handy when you have finished implementing your ePL program and you feel it is ready to be broadcast to the XEL network.
Xeline basically is a wallet software which lets you easily upload your ePL file to the XEL network by just drag-dropping it into the GUI. It takes only a few seconds to have the computation nodes on the XEL network start searching for solutions to your algorithm. Furthermore, this wallet is able to conveniently perform live monitoring of your open tasks and gathers + collects the results that other nodes have found and recorded on the Blockchain.

The installation is straightforward.

* <p> <a href="windows-xeline">Windows </a></p>
* <p> <a href="mac-os-xeline">MacOS </a></p>
* <p> <a href="linux-xeline">Linux </a></p>

-----

Preparing Your ePL File
-----

We will use our demonstration task <a href="https://github.com/xel-software/xeline/blob/master/demos/find_prime.epl">found here</a> in this tutorial. Save it to a file called “my_own_prime_demo.epl”. While this demo is already integrated in the Xeline wallet and can be run right away, we want to create this demo project from scratch here – for learning purposes. At this moment, your ePL file contains just the program logic. However, to submit it to the Blockchain you have to configure a few parameters which we can “metadata. Those parameters tell Xeline how much you are willing to spend for that job, how long it is meant to be running, how many solutions you are interested in, how many iterations your job is meant to run, and so on. We have not yet covered the iteration part, we save that for later. Metadata is added to your ePL file at the top. So go ahead, an add those lines to the top of your ePL program:
