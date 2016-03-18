## Requirements ##

1. You must have Apache2 HTTP server installed.

2. Axis2/C unofficial must be configured **with JSON and `mod_axis2` support**.

To install Axis2/C refer to one of these manuals:

  * [Install Axis2/C unofficial under Linux / Mac OS X / FreeBSD from source code](InstallationManualLinux.md);
  * [Install Axis2/C unofficial under Solaris from source code](InstallationManualSolaris.md);
  * [Install Axis2/C unofficial under Windows using binary tarball](InstallationManualWindowsBinary.md);
  * [Install Axis2/C unofficial under Windows from source code](InstallationManualWindowsSource.md);


## Creating JavaScript client ##

We will use `echo` service to interact with.

1. Create `json-echo` directory inside of your Apache2 HTTP server documents root (usually `/var/www` on Linux).

2. Download [jquery](http://jquery.com/download/). You can use any modern version of jQuery (1.x or 2.x) compressed or uncompressed.

_If you not sure what version to choose, use "compressed, production jQuery 1.x"._

After you download `jquery-x.xx.x(.min).js` rename it into `jquery.js` and place it into `json-echo` directory.

3. Create HTML Front-End and place it as `echo.html` into `json-echo` directory:
```
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>JSON echo example</title>
    <script src="jquery.js" type="text/javascript"></script>
    <script src="echo.js" type="text/javascript"></script>
  </head>
  <body>
    <table style="border: 1px solid silver">
      <tbody>
        <tr>
          <td>Echo string:</td>
          <td><input type="text" id="request" value="Hello World!" /></td>
        </tr>
      </tbody>
    </table>
    <br/>
    <button id="invoke">Invoke</button>
    <br/>
    <br/>
    Result:
    <br/>
    <div style="border: 1px solid silver"><pre id="result" /></div>
  </body>
</html>
```

4. Create JavaScript client implementation and place it as `echo.js` into `json-echo` directory:
```
(function(){

    var resultObject;

    function invokeEcho() {

        var echoString = $("#request")[0].value;

        var request = {
            "echoString": {
                "text": echoString
            }
        };

        var requestInfo = {
            type: "POST",
            contentType: "application/json; charset=utf-8",
            url: "/axis2/services/echo/echoString",
            async: true,
            processData: false,
            dataType: "json",
            data: JSON.stringify(request)
        };


        function onSuccess(result) {
            resultObject.text(result.echoString.text);
            resultObject.css("color", "");
        }

        function onError(none, error) {
            resultObject.text("ERROR: " + error);
            resultObject.css("color", "red");
        }

        jQuery.ajax(requestInfo)
        .success(onSuccess)
        .error(onError);
    }

    $(document).ready(function() {
        $('#invoke').bind("click", invokeEcho);
        resultObject = $('#result');
    });

})();
```

5. Open this web client from browser: http://localhost/json-echo/echo.html.

Click "Invoke" button, you must see result that come from server.

## Download ##

Download client example [here](https://code.google.com/p/axis2c-unofficial/downloads/detail?name=json-echo.7z).