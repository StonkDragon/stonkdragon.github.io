# Installing the Scale Compiler
## With [Dragon](https://github.com/StonkDragon/Dragon)
Using Dragon, you can install the Scale compiler with the following command:
```
$ dragon package install StonkDragon/Scale <version>
```
Where `<version>` is the version you want to install. If you want to install the latest version, you can omit the version argument.

## Building from source
To build the Scale compiler from source, you will need to have [Clang](https://clang.llvm.org/) and [Dragon](https://github.com/StonkDragon/Dragon) installed.
```
$ git clone https://github.com/StonkDragon/Scale
$ cd Scale
$ dragon build
```
This will build the Scale compiler and install Scale to `/opt/Scale/<version>`. The `sclc` binary will then be symlinked to `/usr/local/bin/sclc`.
