# up
up is a small posix compatible Shell function that allows you to quickly traverse up a directory path.  

Installation
------------

up is a simple shell script and can simply be copied into place.  However it will need to be sourced or referenced in some manner by for cd commands to affect the current shell.  The following examples details what is required for some common shells:

ksh

```sh
export FPATH=<replace with directory path you downloaded the up command to>
```

Posix Compliant Method:

```sh
source <path to up script>
```

Example Usage:
--------------

The following will cd into the first matching parent directory called home
```sh
up home
```

The following will cd into the parent directory using a relative index
```sh
up -1
```

The following will cd into the first directory on your current path
```sh
up 0
```

The up command is graceful should the indexes exceed the number of directories in the path.  However to perform strict error checking use
```sh
up --strict -32           # -relative index of -32 should be out of bounds
up --strict 48            # Fixed index of 48 should be again, out of bounds
```

Your current working path might have been the result of following symbolic links, the following will print your current path
```sh
up --verbose .
```

Paths will always be printed using the verbose argument
```sh
up --verbose home
```

The following will traverse your physical path rather than logical / symbolically linked path
```sh
up --physical dev
```

The following will cd into a path read from stdin
```sh
echo /export/home/myuser/projects | up --stdin
```

Many of the traditional shortcuts employed by the shell / cd are also supported
```sh
up -                                # cd into your previous directory
up ~                                # Cd to your home directory
up                                  # Cd to your home directory
```

Specifying any number of dots as the target will move you up to that directory (following UNIX convention of .. identifying immediate parent directory).  E.g. the following will move up 1, 2 and 3 directories respectively:
```sh
up ..
up ...
up ....
```

And of course, full paths are also supported
```sh
up /dev/proc
```
