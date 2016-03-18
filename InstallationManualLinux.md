## 1. Setting up the environment ##

While compiling, starting Axis2/C or any client/service application, AXIS2C\_HOME must points to directory where Axis2/C is installed.

To setup environment variable open terminal emulator and start:

```
echo 'AXIS2C_HOME="/usr/local/axis2c"' | sudo tee -a /etc/environment
```

Then you must relogin or to continue installing Axis2/C within current terminal enter:

```
export AXIS2C_HOME=/usr/local/axis2c
```

## 2. Installing the dependencies ##

### 2.1 Installing build tools ###

To install Axis2/C and json-c you need Autotools and pkg-config.
Autotools is a set of utilities needed to build source code that is checked out from repository. Pkg-config provides interface to query installed libraries. Also you need mercurial and git clients to check out Axis2/C and json-c source code repositories.

To install them all enter (for Ubuntu/Debian):
```
sudo apt-get install automake autoconf libtool pkg-config mercurial git
```

### 2.2 Installing JSON-C ###

If you need JSON support for Axis2/C you must have json-c installed.

> | Note: please don't install json-c from source code tarball it may break your system. |
|:-------------------------------------------------------------------------------------|

To get and install json-c enter those commands:
```
git clone https://github.com/json-c/json-c.git
cd json-c
./autogen.sh
./configure
make
sudo make install
```

### 2.3 Installing Apache2 (optional) ###

Apache2 is required if you plan to call web services from AJAX using `mod_axis2`.

To perform Apache2 installation enter:
```
sudo apt-get install apache2-mpm-prefork apache2-prefork-dev
```

## 3. Obtaining the source code ##

You can check out source code from mercurial repository or use source release from Download section.

**To use source code release** go to [Download section](https://code.google.com/p/axis2c-unofficial/downloads/list?q=axis2c-unofficial-src-*.7z) and get fresh source code archive.

Unpack it using 7z:

```
7z x axis2c-unofficial-src-*.7z
```

**Or to checkout source code from Mercurial repository**:

You need Mercurial client do download source code. If you don't have it you can install it by running this command (for Ubuntu/Debian):

```
sudo apt-get install mercurial
```

Make clone of repository by running this command:
```
hg clone http://code.google.com/p/axis2c-unofficial/ 
```

If you already have clone of repository and want to update enter that command:
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
./configure --prefix=$AXIS2C_HOME --enable-json --with-apache2 --with-apr
```

To configure with other flags append it to command line.

### 4.2 Building and installing ###

Next, build and install Axis2/C and samples:
```
# installing Axis2/C
make -j8
sudo -E make install
echo "$AXIS2C_HOME" | sudo tee /etc/ld.so.conf.d/axis2c.conf
sudo ldconfig
# installing samples
cd samples
./autogen.sh
./configure --prefix=$AXIS2C_HOME --with-axis2=$AXIS2C_HOME/include/axis2-1.6.0
make -j8
sudo -E make install
```

### 4.3 Configuring mod\_axis2 ###

If you don't use mod\_axis2, skip this section.

To configure Apache2 integration module place `axis2.load` and `axis2.conf` into Apache2 module configuration directory (usually `/etc/apache2/mods-available/` on Debian/Ubuntu).

**`axis2.load`**:
```
LoadModule axis2_module /usr/local/axis2c/lib/libmod_axis2.so
```


**`axis2.conf`**:
```
Axis2RepoPath /usr/local/axis2c
Axis2LogFile /var/log/apache2/mod_axis2c.log
Axis2LogLevel info
Axis2ServiceURLPrefix /services
Axis2MaxLogFileSize 5

<Location /axis2>
    SetHandler axis2_module
</Location>
```

Add `AXIS2C_HOME` into Apache2 environment file:

```
echo "export AXIS2C_HOME=$AXIS2C_HOME" | sudo tee -a /etc/apache2/envvars
```

To make Axis2/C log working(optional) start:
```
sudo touch /var/log/mod_axis2c.log
sudo chown www-data /var/log/mod_axis2c.log
```

Enable mod\_axis2 and restart Apache2.

```
sudo a2enmod axis2
sudo service apache2 restart
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