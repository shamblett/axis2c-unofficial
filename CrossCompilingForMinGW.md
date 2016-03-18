0. Install mingw32:
```
sudo apt-get install mingw32 mingw32-binutils mingw32-runtime
```

1. Download [json-c-mingw](https://code.google.com/p/axis2c-unofficial/downloads/list?q=json-c-mingw) and place it into `/opt/mingw-root`.

2. Clone axis2c-unofficial repo.

3. Cross-compilation script:

```
#!/bin/bash

TARGET_HOST=i586-mingw32msvc

export AR=${TARGET_HOST}-ar
export AS=${TARGET_HOST}-as
export LD=${TARGET_HOST}-ld
export NM=${TARGET_HOST}-nm
export CC=${TARGET_HOST}-gcc
export CPP=${TARGET_HOST}-cpp
export GCC=${TARGET_HOST}-gcc
export CXX=${TARGET_HOST}-g++
export RANLIB=${TARGET_HOST}-ranlib

export JSON_CFLAGS="-I/opt/mingw-root/json-c/include/json-c"
export JSON_LIBS="-ljson-c -L/opt/mingw-root/json-c/lib"
./configure --target=${TARGET_HOST} --host=${TARGET_HOST} --prefix=/opt/mingw-root/axis2c

make -j20
make install
```