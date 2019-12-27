---
title: "All you should know about MIME-types"
tags: [programming]
categories: [english, programming]
share-img: /img/mime-types-header.jpg
---

![](/img/mime-types-header.jpg)

> Photo by NordWood Themes on Unsplash

MIME type stands for **“Multipurpose Internet Mail Extensions”** or we can simply call it **“Media Type”**.

Some examples of MIME types:

An HTML file has MIME type of *text/html*

An JPEG image has MIME type of *image/jpeg*

A binary file or file with unknown type may be considered have MIME type as *application/octet-stream*.

## MIME types are different from file extensions

One thing to remember is that MIME types are different from file extensions. While MIME types are **identifying codes which embedded inside inside a file**, file extensions are simply **identifying codes for file names**.

On Unix/Linux OS environment, we can check MIME types of a file with command `file`.

```bash
$ file --mime-type -b <filename>
# Sample:
$ file --mime-type -b an-image.png
image/png
$ file --mime-type -b web.xml
text/xml
```

MIME types is just a way of naming the types for files. There is no strict rule one file with an extension must be a certain MIME type.

There are several ways to determine (or more correctly defined) MIME types of a file.

* Check the file extension and hope that it is accurate. One example is that if we have a file with `.html`, we will consider it has *text/html* MIME type.

* An other way is to check the content of the file and make a guess on it’s type.

An example for the second way is that we have a template file, for example `test.tmpl`. While checking the content, we see a lot of HTML tags, so we guess the file has MIME type of *text/html*.

```bash
$ file --mime-type test.tmpl
test.tmpl: text/html
```

## MIME types are important in web world

Web browsers use MIME types, not file extensions to determine how they should serve content.

Whenever a browser downloads a resource from server, it reads content MIME type from a header tag [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type). With the directive **media-type** from response header, browser could understand what MIME type of the resource is. As a result, browser understands how it should serve the content.

A sample of Content-Type header:

```bash
Content-Type: text/html; charset=UTF-8
```

In this case, the content has type of `text/html` and encoded in `UTF-8`.

### Let give an example of iframe

As we may know, [iframe HTML tag has an attribute named src to input resource URL](https://www.w3schools.com/tags/att_iframe_src.asp).

If the URL is resource of `text/html `type content, it will be shown inside an iframe tag.

If the URL is resource of `application/octet-stream`, the browser does not know how to render it, as a result, the browser chooses downloading the content instead.

## How to modify MIME types for web applications

As mentioned above, MIME types is just a way of naming types for files. There is no strict rule for a file must have which type. We can define the types for our owned services using configuration.

Most cases, web servers have to define a list of MIME types for a list of file extensions.

A sample of such definition file is from httpd :

https://svn.apache.org/viewvc/httpd/httpd/branches/2.4.x/docs/conf/mime.types?view=co

```text
# This file maps Internet media types to unique file extension(s).
# Although created for httpd, this file is used by many software systems
# and has been placed in the public domain for unlimited redisribution.
#
# The table below contains both registered and (common) unregistered types.
# A type that has no unique extension can be ignored -- they are listed
# here to guide configurations toward known types and to make it easier to
# identify "new" types.  File extensions are also commonly used to indicate
# content languages and encodings, so choose them carefully.
#
# Internet media types should be registered as described in RFC 4288.
# The registry is at <http://www.iana.org/assignments/media-types/>.
#
# MIME type (lowercased)			Extensions
# ============================================	==========
# application/1d-interleaved-parityfec
# application/3gpdash-qoe-report+xml
# application/3gpp-ims+xml
# application/a2l
# application/activemessage
# application/alto-costmap+json
# application/alto-costmapfilter+json
# application/alto-directory+json
# application/alto-endpointcost+json
# application/alto-endpointcostparams+json
# application/alto-endpointprop+json
# application/alto-endpointpropparams+json
# application/alto-error+json
# application/alto-networkmap+json
# application/alto-networkmapfilter+json
# application/aml
application/andrew-inset			ez
# application/applefile
application/applixware				aw
# application/atf
# application/atfx
application/atom+xml				atom
application/atomcat+xml				atomcat
# application/atomdeleted+xml
# application/atomicmail
application/atomsvc+xml				atomsvc
# application/atxml
# application/auth-policy+xml
# application/bacnet-xdd+zip
# application/batch-smtp
# application/beep+xml
# application/calendar+json
# application/calendar+xml
# application/call-completion
# application/cals-1840
# application/cbor
# application/ccmp+xml
application/ccxml+xml				ccxml
....
image/png					png
...
text/html					html htm
```

In above example, any file with extension of `.png` has MIME type `image/png`.

As we store this file in our web server, we can modify as we want.

Location for this `mime.types` file is different for each web server.

An Apache server configuration path will be different from a Tomcat server’s location. But the idea will be the same: **We store a file to define what type a certain resource should be served**.

## Determine MIME types using programming languages

In above examples, we use `file` command to determine a file’s MIME type. But in real web application, there are cases we want to check it through source code. Luckily, most modern programming languages have libraries for this.

In Java, we can use classes such as [javax.activation.MimetypesFileTypeMap](https://www.gnu.org/software/classpathx/jaf/javadoc/javax/activation/MimetypesFileTypeMap.html) to map MIME types from a mime.types file.

Or in NodeJS, to set response header with a MIME type, we can use [response.setHeader](https://nodejs.org/api/http.html#http_response_setheader_name_value)

```javascript
// Returns content-type = text/plain
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('ok');
});
```

Just try searching with keyword “<the language> check mime types”, you can search for many libraries to use.

References

https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types

https://askubuntu.com/questions/7517/what-is-the-relationship-between-mime-types-and-file-extensions

https://www.lifewire.com/file-extensions-and-mime-types-3469109


