## 1. Setting up the environment ##

While compiling, starting Axis2/C or any client/service application, AXIS2C\_HOME must points to directory where Axis2/C is installed. Also you must have Axis2/C libs in PATH.

```
AXIS2C_HOME=c:\ws\axis2c
PATH=c:\ws\axis2c\lib
```

You can set these variables in system properties. After setting these variables, You must re-login or reboot windows.


## 2. Installing the dependencies ##

### 2.1 Installing JSON-C ###

If you need JSON support for Axis2/C you must have json-c installed.

Download [compiled json-c](https://code.google.com/p/axis2c-unofficial/downloads/list?&q=json-c) for your arch and unpack archive contents into `c:\ws\` dir.

Edit the `build/win32/configure.in` from `axis2c-unofficial` directory replacing `ENABLE_JSON = 0` to `ENABLE_JSON = 1`.


## 3. Checking out the source code ##

You need Mercurial client do download source code. If you don't have it you can download it [here](http://tortoisehg.bitbucket.org/download/index.html).

Open Visual Studio 2010 command prompt and cd to directory where you want to download axis2c sources.

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

### 4.1 Configuring Axis2/C ###

To build Axis2/C with additional features you must edit the `build\win32\configure.in` file from `axis2c-unofficial` directory replacing `ENABLE_XXXX = 0` to `ENABLE_XXXX = 1`.

Where `ENABLE_XXXX` is one from the list of additional features supported:

| **Feature**                | **Option name**               |
|:---------------------------|:------------------------------|
| JSON support               | `ENABLE_JSON`                 |
| CURL based transport       | `ENABLE_SSL`                  |
| SSL support                | `ENABLE_LIBCURL`              |
| TCP transport support      | `ENABLE_TCP`                  |


### 4.2 Building and installing ###

Next, build and install Axis2/C and samples:
To start building of Axis2/C type:
```
cd build\win32
build install
xcopy /Y /S ..\build\deploy c:\ws\axis2c
```

## 5. Starting Axis2/C ##

To start Axis2/C open command prompt and enter:

```
cd $AXIS2C_HOME\bin
axis2_http_server
```

Open web browser and enter this URL: http://localhost:9090/axis2/services .

You must see loaded services list.