## 1. Setting up the environment ##

While compiling, starting Axis2/C or any client/service application, these environment variables must be set:
```
export AXIS2C_HOME=/usr/local/axis2c
export DYLD_LIBRARY_PATH=$DYLD_LIBRARY_PATH:$AXIS2C_HOME/lib
```

Append these lines into ~/.profile file, and restart terminal.

To disable variable resetting while going to root, please edit sudoers file, using visudo:
```
sudo visudo
```

Add this line after last "Defaults        env\_keep...":
```
Defaults        env_keep += "AXIS2C_HOME"
```


## 2. Installing the dependencies ##

### 2.1 Installing build tools ###

You must have Xcode 4.6.3 and it's developer tools installed.

Also you must have [macports](http://www.macports.org/) installed.

To install Axis2/C and json-c you need Autotools and pkg-config.
Autotools is a set of utilities needed to build source code that is checked out from repository. Pkg-config provides interface to query installed libraries.

To install them all enter:
```
sudo port install automake autoconf libtool pkgconfig
```

Also you need [mercurial](http://mercurial.selenic.com/downloads/) to check out Axis2/C unofficial source code repository.

### 2.2 Installing JSON-C ###

If you need JSON support for Axis2/C you must have json-c installed.

To get and install json-c enter those commands:
```
curl -L https://github.com/json-c/json-c/archive/master.zip -o json-c.zip
unzip json-c.zip
cd json-c-master
./autogen.sh
./configure
make
sudo make install
```

## 3. Obtaining the source code ##

You can check out source code from mercurial repository or use source release from Download section.

**To use source code release** go to [Download section](https://code.google.com/p/axis2c-unofficial/downloads/list?q=axis2c-unofficial-src-*.7z) and get fresh source code archive.

Unpack it using 7z:
```
7z x axis2c-unofficial-src-*.7z
```

**Or to checkout source code from Mercurial repository**:

To make clone of repository run:
```
hg clone http://code.google.com/p/axis2c-unofficial/ 
```

If you already have clone of repository and want to update enter:
```
hg pull -u axis2c-unofficial
```

Next cd to Axis2/C source directory and create autotools scripts:
```
cd axis2c-unofficial
./autogen.sh
```


## 4. Configuring, building and installing ##

### 4.1 Configuring Axis2/C ###

To build Axis2/C with additional features you must append additional configuration flags to standard flag list.

There is the list of additional features supported:

| **Feature**                    | **Additional flags**          |
|:-------------------------------|:------------------------------|
| JSON support                   | `--enable-json`               |
| CURL based transport           | `--enable-libcurl`            |
| SSL support                    | `--enable-openssl`            |
| TCP transport support          | `--enable-tcp`                |
| Disable multi threading        | `--enable-multi-thread=no`    |
| Build mod\_axis2 for Apache2   | `--with-apache2 --with-apr`   |


To perform default configuration of Axis2/C without any additional features enter:
```
./configure --prefix=$AXIS2C_HOME
```

Or if you need to build Axis2/C with JSON support and Apache2 integration module (mod\_axis2) you must have Apache2 installed as in section 2.3. To configure Axis2/C with mod\_axis2 support enter:
```
PKG_CONFIG_PATH+=:/usr/local/lib/pkgconfig ./configure --prefix=$AXIS2C_HOME --enable-json --with-apache2 --with-apr
```

If you building with apache2, you may need to patch apr1 installation:
```
sudo sed -i~ 's:/Applications/.*/usr/bin/\(.*\)$:\1:' /usr/share/apr-1/build-1/libtool /usr/share/apr-1/build-1/apr_rules.mk /usr/share/httpd/build/config_vars.mk
```

To configure with other flags append it to command line.

### 4.2 Building and installing ###

Next, build and install Axis2/C and samples:
```
# installing Axis2/C
make -j8
sudo make install
# installing samples
cd samples
./autogen.sh
./configure --prefix=$AXIS2C_HOME --with-axis2=$AXIS2C_HOME/include/axis2-1.6.0
make -j8
sudo make install
```

### 4.3 Configuring mod\_axis2 ###

If you don't use mod\_axis2, skip this section.

To configure Apache2 integration module place `axis2.conf` into Apache2 module configuration directory (usually `/private/etc/apache2/other/`).

**`/private/etc/apache2/other/axis2.conf`**:
```
LoadModule axis2_module /usr/local/axis2c/lib/libmod_axis2.dylib

Axis2RepoPath /usr/local/axis2c
Axis2LogFile /var/log/apache2/mod_axis2c.log
Axis2LogLevel info
Axis2ServiceURLPrefix /services
Axis2MaxLogFileSize 5

<Location /axis2>
    SetHandler axis2_module
</Location>
```

To make Axis2/C log working(optional) start:
```
sudo touch /var/log/mod_axis2c.log
sudo chown _www:_www /var/log/mod_axis2c.log
```

restart Apache2:

```
sudo apachectl restart
```

After configuration is complete, you must see services list at http://localhost/axis2/services.

## 5. Starting standalone Axis2/C server ##

If you don't use mod\_axis2 you may want to use simple http server.

To start Axis2/C standalone http server enter:

```
cd $AXIS2C_HOME/bin
./axis2_http_server
```

Open web browser and enter this URL: http://localhost:9090/axis2/services .

You must see loaded services list.