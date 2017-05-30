# up

[![GitHub license](https://img.shields.io/badge/license-GPLv3-blue.svg)](https://raw.githubusercontent.com/NeoOrigin/up/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/NeoOrigin/up.svg)](https://github.com/NeoOrigin/up/releases/latest)

up is a small posix compatible Shell function that allows you to quickly traverse up a directory path.  

Installation
------------

up is a simple shell script and can simply be copied into place.  However it will need to be sourced or referenced in some manner for cd commands to affect the current shell.  The following examples details what is required for some common shells:

ksh

```shell
export FPATH=<replace with directory path you downloaded the up command to>
```

Posix Compliant Method:

```shell
source <path to up script>
```

Example Usage:
--------------

The following will cd into the first matching parent directory called home:

```shell
up home
```

With up you can define bookmarks in a text file (configurable with the UP_BOOKMARKS environment variable, value is ~/.up by default). This allows you to save the current directory and cd to it much like how an alias works. For example the following saves the current directory and later goes back:

```shell
pwd
/tmp

up ++
...
up @tmp

pwd
/tmp
```

Or using your own name (mytemp)

```shell
pwd
/tmp

up +mytemp
...
up @mytemp

pwd
/tmp
```

The following will cd into the parent directory using a relative index:

```shell
up -1
```

The following will cd into the root directory /

```shell
up 0
```

The following will cd into the first directory on your current path:

```shell
up 1
```

The up command is graceful should the indexes exceed the number of directories in the path.  However to perform strict error checking use:

```shell
up --strict -32           # -relative index of -32 should be out of bounds
up --strict 48            # Fixed index of 48 should be again, out of bounds
```

Your current working path might have been the result of following symbolic links, the following will print your current path:

```shell
up --verbose .
```

Paths will always be printed using the verbose argument:

```shell
up --verbose home
```

The following will traverse your physical path rather than logical / symbolically linked path

```shell
up --physical dev
```

The following will cd into a path read from stdin

```shell
echo /export/home/myuser/projects | up --stdin
```

Many of the traditional shortcuts employed by the shell / cd are also supported

```shell
up -                                # Cd into your previous directory
up ~                                # Cd to your home directory
up                                  # Cd to your home directory
```

Specifying any number of dots as the target will move you up to that directory (following UNIX convention of .. identifying immediate parent directory).  E.g. the following will move up 1, 2 and 3 directories respectively:

```shell
up ..
up ...
up ....
```

And of course, full paths are also supported:

```shell
up /dev/proc
```
