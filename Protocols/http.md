# HTTP

## HTTP Request

```
GET /books/search.asp?q=wahh HTTP/1.1
Accept: image/gif, image/xxbitmap, image/jpeg, image/pjpeg,
application/xshockwaveflash, application/vnd.msexcel,
application/vnd.mspowerpoint, application/msword, */*
Referer: http://wahh-app.com/books/default.asp
Accept-Language: en-gb,en-us;q=0.5
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)
Host: wahh-app.com
Cookie: lang=en; JSESSIONID=0000tI8rk7joMx44S2Uu85nSWc_:vsnlc502
```

The first line consists of three items:

* A verb indicating the HTTP method.
* The requested URL
* The HTTP version used

Some other points of interest are:

* The `referer` header
* The `user-agent`
* The `host` header which is necessary when multiple websites are hosted on the same server
* The `cookie` header

## HTTP Response

```
HTTP/1.1 200 OK
Date: Sat, 19 May 2007 13:49:37 GMT
Server: IBM_HTTP_SERVER/1.3.26.2 Apache/1.3.26 (Unix)
Set-Cookie: tracking=tI8rk7joMx44S2Uu85nSWc
Pragma: no-cache
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Content-Type: text/html;charset=ISO-8859-1
Content-Language: en-US
Content-Length: 24246
<!DOCTYPE html PUBLIC “-//W3C//DTD HTML 4.01 Transitional//EN”>
<html lang=”en”>
<head>
<meta http-equiv=”Content-Type” content=”text/html;
charset=iso-8859-1”>
```

The first line consists of three items:

* The HTTP version used
* A numeric status code
* A textual phrase further describing the status of response

Some other points of interest:

* The `Server` header
* The `Set-Cookie` issuing the browser a further cookie
* The `Pragma` header instruction the browser not to store the response in its cache
* The `Expires` header 

## HTTP Methods

* GET is designed for retrieval of resources
* POST is designed for performing actions
* HEAD is the same as GET except the server should not return a message body
* TRACE is designed for diagnostic purposes. It can be used to detect the effect of any proxy server in between client and server
* OPTIONS asks the server to report the HTTP methods that are available
* PUT attempts to upload a specific file

## HTTP Headers

### General Headers 

* **Connection** is used to inform the other end whether it should close the TCP connection
* **Content-encoding**
* **Content-length**
* **Content-type** for example `text/html`
* **Transfer-encoding**

### Request Headers

* **Accept** tells the server what king of content the client is willing to accept
* **Accept-encoding**
* **Authorization** is used to submit credentials
* **Cookie** is used to submit cookies
* **Host** specifies the host name
* **If-Modified-Since** specifies the time at which the browser last received the request source. If the resource has not changed since then the server may instruct the client to use its cached copy
* **If-None-Match** specifies an *entity-tag* which is an identifier
* **Referer**
* **User-agent**

### Response Headers

* **Cache-Control** is used to pass caching directives to the browser
* **ETag** specifies an entity tag
* **Expires** instructs the browser how long the contents of the mesage body are valid for
* **Location** is used in redirection responses to specify the target o the redirect
* **Pragma** passes caching directives
* **Server** provides information about the web server software
* **Set-Cookie**
* **WWW-Authenticate** provides details of the types of authentication supported

## Cookies

Cookies normally consist of a name/value pair but may consist of any string that does not contain a space.

In addition to the cookie actual value the `Set-Cookie` header can also include any of the following optional attributes :

* **expires** sets a date until which the cookie is valid
* **domain** specifies the domain for which the cookie is valid
* **path** specifies the URL path for which the cookie is valid
* **secure** allows cookies to be submitted in HTTPS only request
* **HttpOnly** denies JavaScript to directly access the cookie although not all browsers supprot this restriction

## Status Codes

The status codes fall into five groups:

* **1xx** - Informational
* **2xx** - The request was successful
* **3xx** - The client is redirected to a different source
* **4xx** - The request contains an error of some king
* **5xx** - The server encountered an error fulfilling the request

Here are some common status codes:

* **100 Continue** - The client should continue sending the body
* **200 Ok**
* **201 Created** - This is returned in response to `PUT`
* **301 Moved Permanently** - This redirects the browser permanently to a different URL
* **302 Found** - This redirects the browser temporarily to a different URL
* **304 Not Modified** - Instructs the browser to use its cached copy
* **400 Bad Request** - Invalid HTTP request
* **401 Unauthorized**
* **403 Forbidden** - no one is allowed to access the requested resource, regardless of authentication
* **404 Not Found** 
* **405 Method Not Allowed**
* **413 Request Entity Too Large** - If you are probing for buffer overflow
* **414 URI Too Long**
* **500 Internal Server Error**
* **503 Service Unavailable**

## HTTP Authentication

* **Basic** sends user credentials as a Base64 encoded string in a request header 
* **NTLM** is a challenge response mechanism and uses a version of the Windows NTLM protocol
* **Digest** uses MD5 checksums of a nonce with the user's credentials

## Encoding

### URL Encoding

The `%` prefix is followed by the character's two digits ASCII code expressed in hexadecimal.

Example

```
%3d =
%20 space
%0a new line
```

### Unicode encoding

The `%u` prefix followed by the character's Unicode point expressed in hexadecimal. For example `%u2215 /`

### HTML Encoding

Example

```
&quot; "
&apos; '
&lt;   <
&gt;   >
```

In addition any character can be HTML-encoded using its ASCII code in decimal form, for example:

```
&#34; "
&#39; '
```

or by using its ASCII code in hexadecimal form prefixed by an *x*, for example:

```
&#x22 "
&#x27 '
```

### Base64 Encoding

Base64 encoding processes input data in blocks of three bytes. Each of this block is divided into four chunks of six bits each. 2^6 = 64 characters to represent 6 bits.