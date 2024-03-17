# Ubuntu

Ubuntu is a popular Linux distribution based on Debian and composed mostly of free and open-source software that runs from the desktop to the cloud, to all your Internet connected things. It is the world's most popular operating system across public clouds and OpenStack clouds.

[Ubuntu description on Wikipedia](https://wikipedia.org/wiki/Ubuntu)

![ubuntu-new-logo-250x250-1](https://github.com/AppJail-makejails/ubuntu/assets/40880686/f01546b7-72e6-4f30-ab27-53e757143009)

## How to use this Makejail

1. Clone this repository, and cd into the directory that contains the `Makejail` file

In your FreeBSD terminal:

``` 
git clone git clone https://github.com/AppJail-makejails/ubuntu.git appjail-ubunti-demo
cd appjail-ubunti-demo
```

2. Additional env vars and setup:

In your FreeBSD terminal

```
INCLUDE options/network.makejail
INCLUDE gh+AppJail-makejails/ubuntu

ARG ruleset=0

OPTION template=files/linux.conf
OPTION devfs_ruleset=${ruleset}
```

Fetching a base Ubuntu image:

```
pkg install debootstrap
appjail fetch debootstrap jammy
```

3. If you have not done so already. a loopback interface `appjail0` must be set up. Run the three commands `sysrc`, `sysrc` and `service` [on this page](https://appjail.readthedocs.io/en/latest/networking/virtual-networks/alias-and-virtual-networks/)


4. Options to suit your environment should be in `options/network.makejail`. Here is an example of that:

```
ARG network
ARG interface=appjail0

OPTION alias=${interface}
OPTION virtualnet=${network} default
OPTION nat
```


5. Create a `files/linux.conf` template is as follows:

```
exec.start: /bin/true
exec.stop: /bin/true
persist
```

6. Open a shell and run `appjail makejail`:

```sh
appjail makejail -j ubuntu -- --network development --ruleset 11
```

Your ruleset must unhide `shm` and `shm/*`.

7. Logging in to the container

```
appjail start ubuntu
appjail login ubuntu
```
