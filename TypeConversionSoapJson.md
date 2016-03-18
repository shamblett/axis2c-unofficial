## SOAP `<`-`>` JSON Type conversion ##

To represent JSON types and to get source JSON type from AxiOM SOAP "xsi:type" attribute is used.

For string types no "xsi:type" attribute is written.

## Example ##

This is an example of JSON Object and equivalent SOAP Envelope.

### JSON Object: ###
```

{"get": {  /* operation name */
  "string_value": "some string here",
  "boolean_value": true,
  "int_value": 1,
  "double_value": 123.456789,
  "null_value": null,
  "array_of_integers": [1,2,3,4],
  "array_of_strings": ["1","2","3","4"],
  "array_of_objects": [{"str_val":"data", "int_val": 123}],
  "object": {
    "some_int_data": 0,
    "some_data": "some data here"
  }
},
"@headers": { /* SOAP headers (optional) */
  "header1": "header value"
}}

```

### Equivalent SOAP Envelope: ###

```
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Header>
    <s:header1 xmlns:s="urn:json">header value</s:header1>
  </soapenv:Header>
  <soapenv:Body>
    <get xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <string_value>some string here</string_value>
      <boolean_value xsi:type="boolean">true</boolean_value>
      <int_value xsi:type="int">1</int_value>
      <double_value xsi:type="double">123.456789</double_value>
      <null_value xsi:nil="true" />
      <array_of_integers xmlns:enc="http://schemas.xmlsoap.org/soap/encoding/" enc:arrayType="int[4]">
        <item xsi:type="int">1</item>
        <item xsi:type="int">2</item>
        <item xsi:type="int">3</item>
        <item xsi:type="int">4</item>
      </array_of_integers>
      <array_of_strings xmlns:enc="http://schemas.xmlsoap.org/soap/encoding/" enc:arrayType="string[4]">
        <item>1</item>
        <item>2</item>
        <item>3</item>
        <item>4</item>
      </array_of_strings>
      <array_of_objects xmlns:enc="http://schemas.xmlsoap.org/soap/encoding/" enc:arrayType="object[1]">
        <item>
          <str_val>data</str_val>
          <int_val xsi:type="int">123</int_val>
        </item>
      </array_of_objects>
      <object>
        <some_int_data xsi:type="int">0</some_int_data>
        <some_data>some data here</some_data>
      </object>
    </get>
  </soapenv:Body>
</soapenv:Envelope>
```