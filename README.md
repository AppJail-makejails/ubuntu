# Ubuntu

Ubuntu is a popular Linux distribution based on Debian and composed mostly of free and open-source software that runs from the desktop to the cloud, to all your Internet connected things. It is the world's most popular operating system across public clouds and OpenStack clouds.

wikipedia.org/wiki/Ubuntu

![ubuntu-new-logo-250x250-1](https://github.com/AppJail-makejails/ubuntu/assets/40880686/f01546b7-72e6-4f30-ab27-53e757143009)

## How to use this Makejail

```
INCLUDE options/network.makejail
INCLUDE gh+AppJail-makejails/ubuntu

ARG ruleset=0

OPTION template=files/linux.conf
OPTION devfs_ruleset=${ruleset}
```

Where `options/network.makejail` are the options that suit your environment, for example:

```
ARG network
ARG interface=appjail0

OPTION alias=${interface}
OPTION virtualnet=${network} default
OPTION nat
```

In the above example `appjail0` is a loopback interface, so it must first exist before creating the jail.

The `files/linux.conf` template is as follows:

```
exec.start: /bin/true
exec.stop: /bin/true
persist
```

Open a shell and run `appjail makejail`:

```sh
appjail makejail -j ubuntu -- --network development --ruleset 11
```

Your ruleset must unhide `shm` and `shm/*`.

## Notes

* This Makejail uses the `jammy` version of Ubuntu. 
