# Kas files

[![Build Status](http://51.75.135.20:8200/buildStatus/icon?job=kas-files)](http://51.75.135.20:8200/job/kas-files/)

## CI status

|  Board  |  Status |
|:-------:|:-------:|
|    imx7s-warp     |     [![Build Status](http://51.75.135.20:8200/buildStatus/icon?job=imx7s-warp)](http://51.75.135.20:8200/job/imx7s-warp/)    |
|    nitrogen8m     |     [![Build Status](http://51.75.135.20:8200/buildStatus/icon?job=nitrogen8m)](http://51.75.135.20:8200/job/nitrogen8m/)    |
|    raspberrypi3   |     [![Build Status](http://51.75.135.20:8200/buildStatus/icon?job=raspberrypi3)](http://51.75.135.20:8200/job/raspberrypi3/)    |
|    sama5d27-som1-ek-sd   |     [![Build Status](http://51.75.135.20:8200/buildStatus/icon?job=sama5d27-som1-ek-sd)](http://51.75.135.20:8200/job/sama5d27-som1-ek-sd/)    |

## Building an Image

Native Build
------------

On a compatible distribution, install the
[packages](https://www.yoctoproject.org/docs/3.1/mega-manual/mega-manual.html#required-packages-for-the-build-host)
that Yocto 3.1 requires.

Furthermore, install the kas build tool:

```shell
$ sudo pip3 install kas
```

Clone the `kas-files` repository (or unpack an archive of it) into a work
directory:

```shell
$ git clone https://github.com/texierp/kas-files
```

Now you can build an image like this:

```shell
$ kas build kas-files/kas-poky.yml:kas-files/board-<machine name>.yml
```

You can replace `machine name` by the following machine config file:

```
├── board-beaglebone-yocto.yml
├── board-imx7d-pico.yml
├── board-imx7s-warp.yml
├── board-nitrogen8m.yml
├── board-qemuarm-testimage.yml
├── board-raspberrypi3.yml
├── board-raspberrypi4.yml
├── board-sama5d27-som1-ek-sd.yml
├── board-stm32mp157a-dk1.yml
├── docker-raspberrypi3.yml
├── swupdate-raspberrypi3.yml
└── swupdate-sama5d27-som1-ek-sd.yml
```

See after for the `raspberrypi3`:

```shell
$ kas build kas-files/kas-poky.yml:kas-files/board-raspberrypi3.yml
```


Docker Build
------------

Make sure Docker is installed and properly configured for your host system. You
may have to switch the storage driver away from legacy aufs, see
[Docker documentation](https://docs.docker.com/engine/userguide/storagedriver/selectadriver),
if kas warns about this.

Again, the first step is cloning of the repository (or unpacking an archive):

```shell
$ git clone https://github.com/texierp/kas-files
```

Next, install the `kas-container` script like this:

```shell
$ wget https://raw.githubusercontent.com/siemens/kas/master/kas-container
$ chmod a+x kas-container
```

Now you can generate a desired image. The following assumes that your user has
permission to use docker. Usually, this is achieved by adding the user to the
docker group (which has security implications). Note that running the build as
root does not work.

```shell
$ ./kas-container build kas-files/kas-poky.yml:kas-files/board-raspberrypi3.yml
```

The above command disposes the build container after use, keeping downloads and
build results in the current work directory.

Maintainer
----------

- Pierre-Jean Texier
