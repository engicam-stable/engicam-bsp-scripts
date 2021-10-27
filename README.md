# ENGICAM BSP Script

Install Docker Engine on Ubuntu
===============================

First things first: our script utilizes **Docker** in order to assure
the compatibility between Yocto and Ubuntu versions.

To install **Docker** correctly you need to:

**Setup the repository**

Update the apt package index and install the following packages to allow
apt to use a repository over HTTPS:

    sudo apt-get update
    sudo apt-get install apt-transport-https ca-certificates \
    curl gnupg-agent software-properties-common linux-generic

Add Docker\'s official GPG key:

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Verify that you now have the key with the fingerprint **9DC8 5822 9FC7
DD38 854A E2D8 8D81 803C 0EBF CD88**, by searching for the last 8
characters of the fingerprint:

    sudo apt-key fingerprint 0EBFCD88

You should get this same output:

    pub rsa4096 2017-02-22 [SCEA]
        9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88
    uid [ unknown] Docker Release (CE deb) <docker@docker.com>
    sub rsa4096 2017-02-22 [S]

Use the following command to set up the stable repository:

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable"

Install Docker Engine:

    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io

Download and use setup script
=============================

First you need to clone the git repository:

    git clone https://github.com/engicam-stable/engicam-bsp-scripts.git

Go into the directory just created and launch the script to prepare the
environment:

    cd ~/engicam-bsp-scripts
    ./prepare_engicam_bsp --help
    ./prepare_engicam_bsp <branch> <version>

The next table will list all the available environments.

| branch | version              |
|--------|----------------------|
| nxp    | zeus                 |
| nxp    | zeus-2.3             |
| nxp    | gatesgarth           |
| nxp    | hardknott            |
| st     | dunfell              |
| st     | dunfell-5.10_icore   |
| st     | dunfell-5.10_ugea    |

For example:

    ./prepare_engicam_bsp nxp zeus-2.3

or:

    ./prepare_engicam_bsp st dunfell

This procedure may take some time to complete. Once it\'s finished you
can find all source code in the **/yocto** folder.

**Note**: *to return to the same Docker environment you just need to
relaunch the same command used to set it up the first time.*
