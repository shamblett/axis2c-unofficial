## 0. Dependencies ##

If you intent to use VS2010 version, you must have VS2010 redistributable package installed (it will be automatically installed with Visual Studio 2010).

If you intent to use MinGW version you must have MinGW version 3.15.2 installed (from Qt SDK 1.1.4).

## 1. Setting up the environment ##

While starting Axis2/C or any client/service application, AXIS2C\_HOME must points to directory where Axis2/C is installed. Also you must have Axis2/C libs in PATH.

```
AXIS2C_HOME=c:\ws\axis2c
PATH=c:\ws\axis2c\lib
```

You can set these variables in system properties. After setting these variables, You must re-login or reboot windows.

## 2. Downloading and installing Axis2/C ##

Download binary tarball of Axis2/C [here](https://code.google.com/p/axis2c-unofficial/downloads/list?q=axis2c-mingw+OR+axis2c-x86-vs2010+OR+axis2c-x64-vs2010). There are 32-bit and 64-bit versions for VS2010 and 32-bit version for MinGW.

Unpack archive contents into `c:\ws\` directory.

## 3. Starting Axis2/C ##

To start Axis2/C open command prompt and enter:

```
cd $AXIS2C_HOME\bin
axis2_http_server
```

Open web browser and enter this URL: http://localhost:9090/axis2/services .

You must see list of loaded services.