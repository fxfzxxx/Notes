# Ajax Introduction

AJAX is a developer's dream, because you can:

- Read data from a web server - after the page has loaded
- Update a web page without reloading the page
- Send data to a web server - in the background

#### **Example: Button click and display context form other sever without refresh the page**

```html
<!DOCTYPE html>
<html>
<body>

<div id="demo">
  <h2>Let AJAX change this text</h2>
  <button type="button" onclick="loadDoc()">Change Content</button>
</div>

</body>
</html>
```

```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
     document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "ajax_info.txt", true);
  xhttp.send();
}
```

## What is AJAX?

AJAX = **A**synchronous **J**avaScript **A**nd **X**ML.

AJAX is not a programming language.

AJAX just uses a combination of:

- A browser built-in `XMLHttpRequest` object (to request data from a web server)
- JavaScript and HTML DOM (to display or use the data)

**AJAX is a misleading name. AJAX applications might use XML to transport data, but it is equally common to transport data as plain text or JSON text.**

AJAX allows web pages to be updated asynchronously by exchanging data with a web server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

<img src="https://www.w3schools.com/js/pic_ajax.gif" alt="AJAX"  />

## The XMLHttpRequest Object

All modern browsers support the `XMLHttpRequest` object.

The `XMLHttpRequest` object can be used to exchange data with a web server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.


## Create an XMLHttpRequest Object

All modern browsers (Chrome, Firefox, IE7+, Edge, Safari, Opera) have a built-in `XMLHttpRequest` object.

Syntax for creating an `XMLHttpRequest` object:

`var xxx = new XMLHttpRequest();`

## Access Across Domains

For security reasons, modern browsers do not allow access across domains.

This means that both the web page and the XML file it tries to load, must be located on the same server.

The examples on W3Schools all open XML files located on the W3Schools domain.

If you want to use the example above on one of your own web pages, the XML files you load must be located on your own server.

## Modern Browsers (Fetch API)

Modern Browsers can use Fetch API instead of the XMLHttpRequest Object.

The Fetch API interface allows web browser to make HTTP requests to web servers.

If you use the XMLHttpRequest Object, Fetch can do the same in a simpler way.



---

| Method                                | Description                                                  |
| :------------------------------------ | :----------------------------------------------------------- |
| new XMLHttpRequest()                  | Creates a new XMLHttpRequest object                          |
| abort()                               | Cancels the current request                                  |
| getAllResponseHeaders()               | Returns header information                                   |
| getResponseHeader()                   | Returns specific header information                          |
| open(*method, url, async, user, psw*) | Specifies the request  *method*: the request type GET or POST *url*: the file location *async*: true (asynchronous) or false (synchronous) *user*: optional user name *psw*: optional password |
| send()                                | Sends the request to the server Used for GET requests        |
| send(*string*)                        | Sends the request to the server. Used for POST requests      |
| setRequestHeader()                    | Adds a label/value pair to the header to be sent             |

| Property           | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| onreadystatechange | Defines a function to be called when the readyState property changes |
| readyState         | Holds the status of the XMLHttpRequest. 0: request not initialized 1: server connection established 2: request received 3: processing request 4: request finished and response is ready |
| responseText       | Returns the response data as a string                        |
| responseXML        | Returns the response data as XML data                        |
| status             | Returns the status-number of a request 200: "OK" 403: "Forbidden" 404: "Not Found" For a complete list go to the [Http Messages Reference](https://www.w3schools.com/tags/ref_httpmessages.asp) |
| statusText         | Returns the status-text (e.g. "OK" or "Not Found")           |

# AJAX - Send a Request To a Server

## GET or POST?

`GET` is simpler and faster than `POST`, and can be used in most cases.

However, always use POST requests when:

- A cached file is not an option (update a file or database on the server).
- Sending a large amount of data to the server (POST has no size limitations).
- Sending user input (which can contain unknown characters), POST is more robust and secure than GET.

## The url - A File On a Server

The url parameter of the `open()` method, is an address to a file on a server:

xhttp.open("GET", "ajax_test.asp", true);

The file can be any kind of file, like .txt and .xml, or server scripting files like .asp and .php (which can perform actions on the server before sending the response back).

## Synchronous Request

To execute a synchronous request, change the third parameter in the `open()` method to `false`:

```java
xhttp.open("GET", "ajax_info.txt", false);
```

Sometimes async = false are used for quick testing. You will also find synchronous requests in older JavaScript code.

Since the code will wait for server completion, there is no need for an `onreadystatechange` function:

### Example

```javascript
xhttp.open("GET", "ajax_info.txt", false);
xhttp.send();
document.getElementById("demo").innerHTML = xhttp.responseText;
```

Synchronous XMLHttpRequest (async = false) is not recommended because the JavaScript will stop executing until the server response is ready. If the server is busy or slow, the application will hang or stop.

Synchronous XMLHttpRequest is in the process of being removed from the web standard, but this process can take many years.

Modern developer tools are encouraged to warn about using synchronous requests and may throw an InvalidAccessError exception when it occurs.

# AJAX - Server Response

## The onreadystatechange Property

The `readyState` property holds the status of the XMLHttpRequest.

The `onreadystatechange` property defines a function to be executed when the readyState changes.

The `status` property and the `statusText` property holds the status of the XMLHttpRequest object.

| Property           | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| onreadystatechange | Defines a function to be called when the readyState property changes |
| readyState         | Holds the status of the XMLHttpRequest. <br />0: request not initialized <br />1: server connection established<br />2: request received 3: processing request <br />4: request finished and response is ready |
| status             | 200: "OK" 403: "Forbidden" 404: "Page not found" For a complete list go to the [Http Messages Reference](https://www.w3schools.com/tags/ref_httpmessages.asp) |
| statusText         | Returns the status-text (e.g. "OK" or "Not Found")           |

​	

The `onreadystatechange` event is triggered four times (1-4), one time for each change in the readyState.

## Server Response Properties

| Property     | Description                       |
| :----------- | :-------------------------------- |
| responseText | get the response data as a string |
| responseXML  | get the response data as XML data |

## Server Response Methods

| Method                  | Description                                                  |
| :---------------------- | :----------------------------------------------------------- |
| getResponseHeader()     | Returns specific header information from the server resource |
| getAllResponseHeaders() | Returns all the header information from the server resource  |

## The responseXML Property

The XMLHttpRequest object has an in-built XML parser.

The `responseXML` property returns the server response as an XML DOM object.

Using this property you can parse the response as an XML DOM object:

#### Example: Request the file [cd_catalog.xml](https://www.w3schools.com/js/cd_catalog.xml) and parse the response:

```javascript
xmlDoc = xhttp.responseXML;
txt = "";
x = xmlDoc.getElementsByTagName("ARTIST");
for (i = 0; i < x.length; i++) {
  txt += x[i].childNodes[0].nodeValue + "<br>";
}
document.getElementById("demo").innerHTML = txt;
xhttp.open("GET", "cd_catalog.xml", true);
xhttp.send();
```

