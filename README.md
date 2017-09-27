# Docker machine qemu driver

I needed a non-libvirt qemu driver, so this is it.

Its initial use is going to be for running the [Rancher OS](https://github.com/rancher/os) tests, but maybe you'll find a use for it too.


from @fventuri

#### QEMU

Create machines locally using [QEMU](http://www.qemu.org/).
This driver requires QEMU to be installed on your host.

    $ docker-machine create --driver=qemu qemu-test

Options:

 - `--qemu-boot2docker-url`: The URL of the boot2docker image. Defaults to the latest available version.
 - `--qemu-disk-size`: Size of disk for the host in MB. Default: `20000`
 - `--qemu-memory`: Size of memory for the host in MB. Default: `1024`
 - `--qemu-program` : Name of the qemu program to run. Default: `qemu-system-x86_64`
 - `--qemu-network`: Networking to be used: user, tap or bridge. Default: `user`
 - `--qemu-network-interface`: Name of the network interface to be used for networking. Default: `tap0`
 - `--qemu-network-address`: IP of the network address to be used for networking.
 - `--qemu-network-bridge`: Name of the network bridge to be used for networking. Default: `br0`

The `--qemu-boot2docker-url` flag takes a few different forms.  By
default, if no value is specified for this flag, Machine will check locally for
a boot2docker ISO.  If one is found, that will be used as the ISO for the
created machine.  If one is not found, the latest ISO release available on
[boot2docker/boot2docker](https://github.com/boot2docker/boot2docker) will be
downloaded and stored locally for future use.  Note that this means you must run
`docker-machine upgrade` deliberately on a machine if you wish to update the "cached"
boot2docker ISO.

This is the default behavior (when `--qemu-boot2docker-url=""`), but the
option also supports specifying ISOs by the `http://` and `file://` protocols.
`file://` will look at the path specified locally to locate the ISO: for
instance, you could specify `--qemu-boot2docker-url
file://$HOME/Downloads/rc.iso` to test out a release candidate ISO that you have
downloaded already.  You could also just get an ISO straight from the Internet
using the `http://` form.

Environment variables:

Here comes the list of the supported variables with the corresponding options. If both environment
variable and CLI option are provided the CLI option takes the precedence.

| Environment variable              | CLI option                        |
|-----------------------------------|-----------------------------------|
| `QEMU_BOOT2DOCKER_URL`            | `--qemu-boot2docker-url`          |
