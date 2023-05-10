# Ubuntu

Ubuntu is a popular Linux distribution based on Debian and composed mostly of free and open-source software that runs from the desktop to the cloud, to all your Internet connected things. It is the world's most popular operating system across public clouds and OpenStack clouds.

wikipedia.org/wiki/Ubuntu

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/Ubuntu-logo-2022.svg/1920px-Ubuntu-logo-2022.svg.png" width="60%" height="auto" alt="ubuntu logo">

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