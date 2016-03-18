1. install Android NDK

2. Create standalone android toolchain:

```
sudo android-ndk-*/build/tools/make-standalone-toolchain.sh --platform=android-8 --install-dir=/opt/android-8-toolchain
```

3. Clone axis2-unofficial repository:
```
hg clone https://code.google.com/p/axis2c-unofficial/
cd axis2c-unofficial
```

4. Compile and install Axis2/C-unofficial:

```
export TOOLCHAIN_PATH=/opt/android-8-toolchain
export PATH=$PATH:$TOOLCHAIN_PATH/bin/
export AR=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-ar
export AS=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-as
export LD=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-ld
export NM=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-nm
export CC=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-gcc
export CPP=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-cpp
export GCC=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-gcc
export CXX=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-g++
export RANLIB=$TOOLCHAIN_PATH/bin/arm-linux-androideabi-ranlib

./configure --host=arm-linux-gnu --prefix=/data/local/axis2c

sudo mkdir -p /data/local
sudo chmod 777 /data/local
make -j8
make install
```

Android binaries will be placed into `/data/local/axis2c`.