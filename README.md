# ENGICAM BSP RELEASE

## Install Docker Engine on Ubuntu

### Set up the repository

Update the apt package index and install packages to allow apt to use a repository over HTTPS:

    $ sudo apt-get update

    $ sudo apt-get install apt-transport-https ca-certificates \
        curl gnupg-agent software-properties-common

Add Docker’s official GPG key:

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.

    $ sudo apt-key fingerprint 0EBFCD88

    pub   rsa4096 2017-02-22 [SCEA]
          9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
    uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
    sub   rsa4096 2017-02-22 [S]

Use the following command to set up the stable repository:

    $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable"

Install Docker Engine:

    $ sudo apt-get update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io


## first build

at the end of procedure under /yocto folder you can found all source code.


## Set enviroment variables

Enter Yocto folder and launch the script setting enviroment variables:

	DISTRO=<distro name> MACHINE=<machine name> source imx-setup-release.sh -b <build dir>

where ``<machine-name>`` corresponds to the module for which the operative system image will be compiled and ``<build-dir-name>`` is the bulding directory name chosen by the user, as in the following example:

	 DISTRO=eng-imx-xwayland MACHINE=imx8mp-icore source imx-setup-release.sh -b build

where a directory named ``build`` is created and enviroment variables are set to compile images for the module ``i.Core MX8M Plus``. Please notice that the available ``<machine-name>`` correspond to the names of the relative configuration files in ``/sources/meta-engicam-mx8/conf/machine``.

If the build directory already exists due to previous compilations it will be required to set the enviroment variables only executing the command:

	source setup-environment build

## Configure yocto layers

Add with bitbake the meta-engicam-mx8 layer to the image layers:

	bitbake-layers add-layer ../sources/meta-engicam-nxp

## Compile and flash image on sdcard

Compile the desired image with bitbake using the command (in this example we compile the recipe ``engicam-image-qt-multimedia.bb`` for ``i.Core MX8M Plus``):

	bitbake engicam-evaluation-image

Once the image is compiled it will be possible to find in the build directory a deploy folder with the image files. The relative path to this folder from the yocto directory will be:

	tmp/deploy/images/imx8mp-icore
