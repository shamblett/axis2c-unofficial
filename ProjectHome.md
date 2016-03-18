# The project has been moved to GitHub: https://github.com/loentar/axis2c-unofficial #

## Project description ##

Axis2/C is a great software: it's fast, supports most of WS-`*` specifications, it has many features. But unfortunately it have many issues like thread safety, [memory leaks](MemoryLeaksFixed.md) and can't be used in production.

The goal of this project is to provide stable build of Axis2/C that can be used in production. Also we implemented some features that users wanted to have, but Axis2/C team refused to implement.

Axis2/C-unofficial is based on Axis2/C-1.6.0 (which is last released version) and has 100% source compatibility with it.

## New features ##
  * Support for JSON transport - mapped convention;
  * MinGW support (can [build under Windows using MinGW](InstallationManualWindowsSourceMinGW.md), and also [cross-compilation for Windows target under Linux](CrossCompilingForMinGW.md) is supported);
  * [Android support](CompileForAndroid.md);
  * libcurl support for other auth types (not just basic). New types of authentication added: Negotiate, Ntlm, Any, AnySafe

## Applied patches/Fixed bugs ##

> See full list of [issues fixed](IssuesList.md).

## Project News ##
  * May 27, 2014: Implemented support of JSON basic types, see TypeConversionSoapJson for details.
  * Mar 3, 2014: Soap headers can be created from JSON request when adding "@headers" object.
  * Feb 18, 2014: Fixed using of chdir while enumerating services and modules: [issue 6](https://code.google.com/p/axis2c-unofficial/issues/detail?id=6).
  * Feb 4, 2014: Fixed datetime calculations (local to UTC).
  * Jan 3, 2014: Fixed closing stderr while closing log on the client side.
  * Oct 15, 2013: Fixed crash in uuid\_gen\_unix in Solaris 11.
  * Aug 05, 2013: Source tarball of 0e7108ceb231 is available from [Download section](https://code.google.com/p/axis2c-unofficial/downloads/detail?name=axis2c-unofficial-src-0e7108ceb231.7z).
  * Jun 25, 2013: Added support for Apache 2.4.
  * Jun 04, 2013: Added example on how to create [JavaScript JSON client](ExampleJsonEchoClient.md).
  * May 09, 2013: Added script to [build axis2c-unofficial for Android](CompileForAndroid.md).
  * May 02, 2013: Source code and windows binaries changeset 7acae470da50 are available from [download section](https://code.google.com/p/axis2c-unofficial/downloads/list?q=7acae470da50). <br><b>Fixed <a href='MemoryLeaksFixed.md'>memory leaks</a> and <a href='IssuesList.md'>server crash</a> on high load.</b>
<ul><li>Apr 23, 2013: Fixed <a href='https://code.google.com/p/axis2c-unofficial/source/detail?r=12eb18728123a1fba67c44983a8e4839066297cb'>server crash</a> under high load (non thread-safe ctime was replaced to thread-safe code).<br>
</li><li>Apr 14, 2013: Fixed many <a href='MemoryLeaksFixed.md'>memory leaks</a>.<br>
</li><li>Apr 9, 2013: Added support for MinGW: Binary package is <a href='https://code.google.com/p/axis2c-unofficial/downloads/list?q=axis2c-mingw'>here</a>, Installation manual is <a href='InstallationManualWindowsBinary.md'>here</a>;<br>
</li><li>Apr 5, 2013: Added libcurl support for other auth types (not just basic);<br>
</li><li>Apr 4, 2013: Added JSON support - mapped convention;<br>
</li><li>Mar 30, 2013: Initial import and applying basic patches.</li></ul>


<h2>Installation manuals</h2>

<ul><li>How to install axis2c-unofficial under Linux <a href='InstallationManualLinux.md'>from source code</a>;<br>
</li><li>How to install axis2c-unofficial under Windows: <a href='InstallationManualWindowsBinary.md'>from binary tarball</a> or <a href='InstallationManualWindowsSource.md'>from source code</a>;<br>
</li><li>How to install axis2c-unofficial under <a href='InstallationManualSolaris.md'>SunOS/Solaris</a>;<br>
</li><li>How to <a href='CompileForAndroid.md'>compile for Android</a>.</li></ul>

<h2>Support</h2>

Visit the <a href='https://groups.google.com/forum/?fromgroups#!forum/axis2c-unofficial'>groups axis2c-unofficial</a>.<br>
<br>
<h2>Help this project</h2>

If you want to help this project but not sure what you can do, see how to <a href='HowToHelpThisProject.md'>help this project</a>.