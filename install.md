# Installing the Scale Compiler
To install the Scale Compiler, just execute the following commands:
```
$ git clone https://github.com/StonkDragon/Scale
$ cd Scale
$ clang++ -o install-sclc install-sclc.cpp -std=gnu++17
$ sudo ./install-sclc
```
This will install Scale and it's dependencies to `/opt/Scale/<version>`. The `sclc` binary will then be symlinked to `/usr/local/bin/sclc`.
