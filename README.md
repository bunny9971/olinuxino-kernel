# olinuxino-kernel
OLinuXino kernel development container

## Building kernel using default config

Create new directory for kernel and modules

    $ mkdir /tmp/new-kernel

Run docker container

    $ docker run --rm -v /tmp/new-kernel:/data droid4control/olinuxino-kernel

### Different kernel version

Default kernel version is 3.18.13. You can compile any kernel version using environment variable "VERSION"

    $ docker run --rm -v /tmp/new-kernel:/data -e VERSION=3.18.13 droid4control/olinuxino-kernel

### Own config

This docker container has one config file included. To use your own config file just copy it to the /data directory

    $ cp myconfig /tmp/new-kernel/config

NB! This file will be overwritten with actual config (after use of menuconfig)

### Build manually with menuconfig

    $ docker run --rm -ti -v /tmp/new-kernel:/data droid4control/olinuxino-kernel

### Multiple builds

Do not use "--rm" flag to build more than once using the same runnig container (download kernel source once)

    $ docker run --name=mybuild -ti -v /tmp/new-kernel:/data droid4control/olinuxino-kernel /bin/true
    $ docker start mybuild

Enter to the container and run "/root/build.sh" or commands manually

    $ docker exec -ti mybuild /bin/bash
    # /root/build.sh

Remove container afterwards

    $ docker stop mybuild
    $ docker rm mybuild

## Building your own docker container

To build your own container just fork this repository or clone it

    $ git clone https://github.com/droid4control/olinuxino-kernel
    $ cd olinuxino-kernel
    $ docker build -t olinuxino-kernel .
