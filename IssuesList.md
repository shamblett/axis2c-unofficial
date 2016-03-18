## General info ##

Axis2c-unofficial is based on Axis2/C-1.6.0 - most stable release.

There are three types of patches:
  * backports from official trunk;
  * that exists in AXIS2C JIRA but not applied to current official trunk;
  * implemented by our team (marked with `*`).

## List of issues fixed ##

### General bugs: ###
| **Tag**       | **Description** |
|:--------------|:----------------|
| server crash `*` | Fixed [server crash](https://code.google.com/p/axis2c-unofficial/source/detail?r=12eb18728123a1fba67c44983a8e4839066297cb) under high load in axis2\_http\_worker\_process\_request() |
| libcurl auth `*` | libcurl support for other auth types (not just basic) |
| REST POST as GET `*` | Fixed reading size of content when doing REST method POST as GET |
| JSON support `*` | Added support for JSON |
| -Werror `*`   | Axis2/C won't compile on modern compilers |
| neethi test `*` | Axis2/C won't compile because `neethi test` fails to compile |
| UTF-8         | UTF-8 is not supported by guththilla |
| double http auth | Bug: double request is sent in HTTP authenticated clients |
| REST DELETE   | REST DELETE method causes internal server error |

### By platform support: ###
| **Tag**       | **Description** |
|:--------------|:----------------|
| MinGW `*`     | Unable to compile Axis2/C under MinGW environment |
| MacOSX `*`    | Unable to compile Axis2/C under Mac OS X |
| Solaris/SunOS `*` | Unable to compile Axis2/C under Solaris/SunOS |
| Android `*`   | Unable to compile for Android OS |

### Memory leaks fixed: ###

See [full list](MemoryLeaksFixed.md) of memory leaks fixed.

<br>

<h2>TODO: Known issues to fix</h2>

<h3>General bugs</h3>
<table><thead><th> <b>Tag</b>       </th><th> <b>Description</b> </th></thead><tbody>
<tr><td> Client-asynch    </td><td> client crash in asynchronous mode under high load </td></tr></tbody></table>

<h3>Memory leaks:</h3>

Fix all <a href='https://code.google.com/p/axis2c-unofficial/wiki/MemoryLeaksFixed#Known_memleaks_to_fix'>known memleaks</a>.