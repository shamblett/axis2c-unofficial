## 1. Setting up the environment ##

While compiling, starting Axis2/C or any client/service application, AXIS2C\_HOME must points to directory where Axis2/C is installed. Also you must have Axis2/C libs in PATH.

```
AXIS2C_HOME=c:\ws\axis2c
PATH=c:\ws\axis2c\lib
```

You can set these variables in system properties. After setting these variables, You must re-login or reboot windows.

You must have MinGW with Msys installed. Also it's needed to edit environment variable PATH to MinGW and Msys binaries was _before_ any "Windows" directories. For example you must have _system_ PATH environment as below:

```
C:\MinGW\msys\1.0\bin;C:\QtSDK\mingw\bin;%SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;....
```

To be sure, your settings are right, start `bash.exe` and type:
```
find -version
```

it must outputs:
```
find (GNU findutils) <SOME.VERSION.HERE>
```

Also you need to have autotools installed. If you can't find autotools for MinGW you can start `./autogen.sh` script under Linux, then move that directory to Windows.

## 2. Installing the dependencies ##

### 2.1 Installing JSON-C ###

If you need JSON support for Axis2/C you must have json-c installed.

Download [compiled json-c](https://code.google.com/p/axis2c-unofficial/downloads/list?&q=json-c-mingw) and unpack archive contents into `c:\ws\` dir.


## 3. Checking out the source code ##

### 3.1 Using source tarball ###

Download [source tarball](https://code.google.com/p/axis2c-unofficial/downloads/list?q=axis2c-unofficial-src-*.7z) and unpack it.

Go into Axis2/C source dir:
```
cd axis2c-unofficial
```


### 3.2 Checking out from Mercurial repo ###

You need Mercurial client do download source code. If you don't have it you can download it [here](http://tortoisehg.bitbucket.org/download/index.html).

Start bash.exe and cd to directory where you want to download axis2c sources.

Make clone of repository by running this command from command prompt:
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

If you checked source code from Mercurial repo, create autotools scripts:
```
./autogen.sh
cd samples
./autogen.sh
cd -
```


### 4.2 Configuring Axis2/C ###

To build Axis2/C you must modify AXIS2C\_HOME environment variable from Windows to Unix path notation:

```
export AXIS2C_HOME=c:/ws/axis2c
```

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

Or if you need to build Axis2/C with JSON support enter:
```
export JSON_CFLAGS="-Ic:/ws/json-c-mingw/include/json-c"
export JSON_LIBS="-ljson-c -Lc:/ws/json-c-mingw/lib" 
./configure --prefix=$AXIS2C_HOME --enable-json
```

To configure with other flags append it to command line.

### 4.3 Building and installing ###

Next, build and install Axis2/C and samples:
```
make -j8
make install
cd samples
./configure --prefix=$AXIS2C_HOME --with-axis2=$AXIS2C_HOME/include/axis2-1.6.0
make -j8
make install
```


## 5. Starting Axis2/C ##

To start Axis2/C enter:

```
cd $AXIS2C_HOME/bin
./axis2_http_server
```

Open web browser and enter this URL: http://localhost:9090/axis2/services .

You must see list of loaded services.