# Packet Images

Within this repo you will find a collection of tools, examples and docs for building 
OS images to be used on Packet.net baremetal servers.

  - Building images from Dockerfile
  - Converting Docker images for use on physical baremetal servers
  - Building images from Packer.io (coming soon!)

TLDR:  Build docker image, save docker image to archive and convert the archive to a rootfs
image. The image can be used on a baremetal physical server with or without docker.

### Dependencies
There is only a small list of deps required to run image builds, but we recommend a dedicated
machine or VM for this purpose simply to keep things isolated.

 - Docker 1.1.11 and above (older version may work)
 - JQ (will be installed automatically)
 - A linux docker host on top of CentOS7 / Ubuntu 16

### Installation
**Using git:**

    sudo su -
    git clone git@github.com:packethost/packet-images.git
    cp ./tools/packet-save2image /usr/bin/
    chmod u+x /usr/bin/packet-save2image

**or**

**Using wget**

    sudo su -
    wget -O /usr/bin/packet-save2image https://raw.githubusercontent.com/packethost/packet-images/master/tools/packet-save2image
    chmod u+x /usr/bin/packet-*
    
### Example image build
Here we are walking through an example docker image build, docker image save and conversion. It really is that easy!

    [root@buildbox ubuntu1604]# docker build -t ubuntu1604 .
    ...snip...
    Removing intermediate container 31c25fadd64f
    Successfully built dc3183bbe31e
    [root@buildbox ubuntu1604]# docker save ubuntu1604 > ubuntu1604.tar
    [root@buildbox ubuntu1604]# save2image ubuntu1604.tar
    Creating consolidated image archive...
    ....................................................
    Total bytes written: 534384640 (510MiB, 27MiB/s)
    Image archive ubuntu1604.tar-image.gz created successfully
    
### Deploying your custom image on Packet
You have a working image built, so now what? As we work to build our community image site, this part is currently experimental and we are accepting BETA testers. Please contact help@packet.net

### TODOs

 - Add Packer.io Docker plugin and templates
 - More to come


