| Notice: All these instructions where tested under SunOS 5.10 32 bit with a SPARC architecture, if you find any problems installing it please let us know |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------|

## 1. Setting up the environment ##

While compiling, starting Axis2/C or any client/service application, AXIS2C\_HOME must points to directory where Axis2/C is installed.

To setup environment variable open terminal emulator and start:

```
echo 'AXIS2C_HOME="/usr/local/axis2c"' | sudo tee -a /etc/profile
```

Then you must relogin or to continue installing Axis2/C within current terminal enter:

```
export AXIS2C_HOME=/usr/local/axis2c
```

| Notice: If you don't have sudo installed you must run the commands that need privileges as root. |
|:-------------------------------------------------------------------------------------------------|

## 2. Installing the dependencies ##

To install Axis2/C you need bash, binutils, Autotools and pkg-config.
Autotools is a set of utilities needed to build source code that is checked out from repository. Pkg-config provides interface to query installed libraries. Also you need a mercurial client to check out Axis2/C source code repository.

Getting this packages varies depending if you're using a licensed distribution or not.
Free versions of the packages are available here: http://sunfreeware.com/

_Dependencies_

| _**Mandatory**_ |
|:----------------|
| bash            |
| gcc             |
| binutils        |
| pkg-config      |
| _**Optional**_  |
| mercurial       |
| sudo            |
| aclocal         |
| autoheader      |
| autoconf        |
| automake        |
| libtool         |


## 3. Checking out the source code ##

You need Mercurial client do download source code.

Make clone of repository by running this command:
```
hg clone http://code.google.com/p/axis2c-unofficial/ 
```

If you already have clone of repository and want to update enter that command:
```
hg pull -u axis2c-unofficial
```

Next cd to Axis2/C source dir:
```
cd axis2c-unofficial
```

## 4. Configuring, building and installing ##

### 4.1 Generating autotools scripts ###

To create autotools scripts enter:
```
./autogen.sh
```

| Notice: If you don't have autotools (aclocal,autoconf,automake,libtool) in your Solaris machine, you can still generate your configure script in another machine with autotools and pass it to Solaris (the configure is platform independent) |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

### 4.2 Configuring Axis2/C ###

To build Axis2/C with additional features you must append additional configuration flags to standard flag list.

There is the list of additional features supported:

| **Feature**                | **Additional flags**          |
|:---------------------------|:------------------------------|
| JSON support               | `--enable-json`               |
| CURL based transport       | `--enable-libcurl`            |
| SSL support                | `--enable-openssl`            |
| TCP transport support      | `--enable-tcp`                |
| Disable multi threading    | `--enable-multi-thread=no`    |


To perform standard configuration of Axis2/C enter:
```
./configure --prefix=$AXIS2C_HOME
```

Or if you need to build Axis2/C with libcurl transport enabled enter:
```
./configure --prefix=$AXIS2C_HOME --enable-libcurl
```

To configure with other flags append it to command line.

### 4.3 Building and installing ###

Next, build and install Axis2/C and samples:
```
bash
make -j8
sudo make install
sudo crle -u -l "$AXIS2C_HOME"
cd samples
./autogen.sh
CFLAGS=-I$AXIS2C_HOME/include/axis2-1.6.0 LDFLAGS=-L$AXIS2C_HOME/lib ./configure --prefix=$AXIS2C_HOME
make -j8
sudo make install
```


## 5. Starting Axis2/C ##

To start Axis2/C enter:

```
cd $AXIS2C_HOME/bin
./axis2_http_server
```

Open web browser and enter this URL: http://localhost:9090/axis2/services .