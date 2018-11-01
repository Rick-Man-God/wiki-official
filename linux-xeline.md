<!-- TITLE: Linux Xeline -->
<!-- SUBTITLE: A quick summary of Linux Xeline -->

![Xelbig](/uploads/xeline/xelbig.png "Xelbig"){.pagelogo}
# Linux - xeline tutorial
-----

Install from binary
-----


```text
# Make sure unzip is installed
sudo apt-get install -y unzip
​
# Download the latest linux zip archive from:
https://github.com/xel-software/xeline/releases/latest
​
# Unzip the downloaded zip archive
unzip xeline-linux.zip
​
# Go into the directory containing the binary and launch it
cd Xeline-linux-x64
./Xeline
```


Install from source:
-----

```text
# Make sure curl and git are installed
sudo apt-get install -y curl git
​
# Install a recent version of nodejs first, if you haven't already.
#For Ubuntu/Debian is works like this
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt-get install -y nodejs
​
# Get the repository
git clone https://github.com/xel-software/xeline.git
​
# Or if you already have it, cd into the directory containing your xeline sources and update the code
cd xeline
git pull
​
# Now, go into the directory containing your xeline sources and install all dependencies
# (needs to be done only once)
cd xeline
npm install
​
# And finally, run the application
npm start
```

Video tutorial
-----
<div style="width:100%;height:0px;position:relative;padding-bottom:63.529%;"><iframe src="https://streamable.com/s/wqejg/sdkjrz" frameborder="0" width="100%" height="100%" allowfullscreen style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe></div>



