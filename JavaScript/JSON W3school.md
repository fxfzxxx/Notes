# JSON - Introduction

JSON: **J**ava**S**cript **O**bject **N**otation.

JSON is a syntax for storing and exchanging data.

JSON is text, written with JavaScript object notation.

## Exchanging Data

When exchanging data between a browser and a server, the data can only be text.

JSON is text, and we can convert any JavaScript object into JSON, and send JSON to the server.

We can also convert any JSON received from the server into JavaScript objects.

This way we can work with the data as JavaScript objects, with no complicated parsing and translations.

## Sending Data

If you have data stored in a JavaScript object, you can convert the object into JSON, and send it to a server:

```javascript
var myObj = {name: "John", age: 31, city: "New York"};
var myJSON = JSON.stringify(myObj);
window.location = "demo_json.php?x=" + myJSON;
```

## Receiving Data

If you receive data in JSON format, you can convert it into a JavaScript object:

```javascript
var myJSON = '{"name":"John", "age":31, "city":"New York"}';
var myObj = JSON.parse(myJSON);
document.getElementById("demo").innerHTML = myObj.name;
```

## What is JSON?

- JSON stands for **J**ava**S**cript **O**bject **N**otation
- JSON is a lightweight data-interchange format
- JSON is "self-describing" and easy to understand
- JSON is language independent *****

>*
>JSON uses JavaScript syntax, but the JSON format is text only.
>Text can be read and used as a data format by any programming language.

## Why use JSON?

Since the JSON format is text only, it can easily be sent to and from a server, and used as a data format by any programming language.

JavaScript has a built in function to convert a string, written in JSON format, into native JavaScript objects:

```javascript
JSON.parse()
```

So, if you receive data from a server, in JSON format, you can use it like any other JavaScript object.

# JSON Syntax

## JSON Data - A Name and a Value

JSON data is written as name/value pairs.

A name/value pair consists of a field name (in double quotes), followed by a colon, followed by a value:

```javascript
"name":"John" // JSON
{ name:"John" } // JavaScript
```

> JSON names require double quotes. JavaScript names don't.

## JSON Values

In **JSON**, *values* must be one of the following data types:

- a string
- a number
- an object (JSON object)
- an array
- a boolean
- null

In **JavaScript** values can be all of the above, plus any other valid JavaScript expression, including:

- a function
- a date
- undefined

# JSON vs XML

Both JSON and XML can be used to receive data from a web server.

JSON:

```json
{"employees":[
    {"firstName":"John","lastName":"Doe"},
    {"firstName":"Anna","lastName":"Smith"},
    ...
]}
```

XML:

```xml
<employees>
    <employee>
  	  <firstName>John</firstName> <lastName>Doe</lastName>        
    </employee>
	<employee>
  	  <firstName>Anna</firstName> <lastName>Smith</lastName>   
    </employee>
```

## JSON is Like XML Because

- Both JSON and XML are "self describing" (human readable)
- Both JSON and XML are hierarchical (values within values)
- Both JSON and XML can be parsed and used by lots of programming languages
- Both JSON and XML can be fetched with an XMLHttpRequest

## JSON is Unlike XML Because

- JSON doesn't use end tag
- JSON is shorter
- JSON is quicker to read and write
- JSON can use arrays

**The biggest difference is:**

**XML has to be parsed with an XML parser. JSON can be parsed by a standard JavaScript function.**

## Why JSON is Better Than XML

XML is much more difficult to parse than JSON.
JSON is parsed into a ready-to-use JavaScript object.

For AJAX applications, JSON is faster and easier than XML:

Using XML

- Fetch an XML document
- Use the XML DOM to loop through the document
- Extract values and store in variables

Using JSON

- Fetch a JSON string
- JSON.Parse the JSON string

# JSON.parse()

A common use of JSON is to exchange data to/from a web server.

When receiving data from a web server, the data is always a string.

Parse the data with `JSON.parse()`, and the data becomes a JavaScript object.

```javascript
'{ "name":"John", "age":30, "city":"New York"}' //Text form sever
```

Use the JavaScript function `JSON.parse()` to convert text into a JavaScript object:

```javascript
var obj = JSON.parse('{ "name":"John", "age":30, "city":"New York"}');
```

```html
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = obj.name + ", " + obj.age;
</script>
```

## JSON From the Server

You can request JSON from the server by using an AJAX request

As long as the response from the server is written in JSON format, you can parse the string into a JavaScript object.

```javascript
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    var myObj = JSON.parse(this.responseText);
    document.getElementById("demo").innerHTML = myObj.name;
  }
};
xmlhttp.open("GET", "json_demo.txt", true);
xmlhttp.send();

```

## Array as JSON

When using the `JSON.parse()` on a JSON derived from an array, the method will return a JavaScript array, instead of a JavaScript object.

```javascript
var xmlhttp = new XMLHttpRequest();
xmlhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    var myArr = JSON.parse(this.responseText);
    document.getElementById("demo").innerHTML = myArr[0];
  }
};
xmlhttp.open("GET", "json_demo_array.txt", true);
xmlhttp.send();
```

 [json_demo_array.txt](https://www.w3schools.com/js/json_demo_array.txt)

# JSON.stringify()

A common use of JSON is to exchange data to/from a web server.

When sending data to a web server, the data has to be a string.

Convert a JavaScript object into a string with `JSON.stringify()`.

```javascript
var obj = { name: "John", age: 30, city: "New York" };
var myJSON = JSON.stringify(obj);

var arr = [ "John", "Peter", "Sally", "Jane" ];
var myJSON = JSON.stringify(arr);

var obj = { name: "John", today: new Date(), city : "New York" };
var myJSON = JSON.stringify(obj);


```

# JSON Objects

```javascript
{ "name":"John", "age":30, "car":null }
x = myObj.name;
x = myObj["name"];

for (x in myObj) {
  document.getElementById("demo").innerHTML += x;
}
/** Nested */
myObj = {
  "name":"John",
  "age":30,
  "cars": {
    "car1":"Ford",
    "car2":"BMW",
    "car3":"Fiat"
  }
 }

x = myObj.cars.car2;
x = myObj.cars["car2"];

myObj.cars.car2 = "Mercedes";
myObj.cars["car2"] = "Mercedes";
```

# JSON Arrays

```javascript
[ "Ford", "BMW", "Fiat" ]

{
"name":"John",
"age":30,
"cars":[ "Ford", "BMW", "Fiat" ]
}
x = myObj.cars[0];

for (i in myObj.cars) {
  x += myObj.cars[i];
}

for (i = 0; i < myObj.cars.length; i++) {
  x += myObj.cars[i];
}
/** nested   */
myObj = {
  "name":"John",
  "age":30,
  "cars": [
    { "name":"Ford", "models":[ "Fiesta", "Focus", "Mustang" ] },
    { "name":"BMW", "models":[ "320", "X3", "X5" ] },
    { "name":"Fiat", "models":[ "500", "Panda" ] }
  ]
 }

for (i in myObj.cars) {
  x += "<h1>" + myObj.cars[i].name + "</h1>";
  for (j in myObj.cars[i].models) {
    x += myObj.cars[i].models[j];
  }
}
```

# JSONP

JSONP is a method for sending JSON data without worrying about cross-domain issues.

JSONP does not use the `XMLHttpRequest` object.

JSONP uses the `<script>` tag instead.

## JSONP Intro

JSONP stands for JSON with Padding.

Requesting a file from another domain can cause problems, due to cross-domain policy.

Requesting an external *script* from another domain does not have this problem.

JSONP uses this advantage, and request files using the script tag instead of the `XMLHttpRequest` object.

```javascript
<script src="demo_jsonp.php">
```

## The Server File

The file on the server wraps the result inside a function call:

```php+HTML
<?php
$myJSON = '{ "name":"John", "age":30, "city":"New York" }';

echo "myFunc(".$myJSON.");";
?>
```

## The JavaScript function

The function named "myFunc" is located on the client, and ready to handle JSON data:

```javascript
function myFunc(myObj) {
  document.getElementById("demo").innerHTML = myObj.name;
}
```

```javascript
function clickButton() {
  var s = document.createElement("script");
  s.src = "demo_jsonp.php";
  document.body.appendChild(s);
}
```

