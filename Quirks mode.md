
In the old days of web, websites were written in 2 versions, one for `Netscape Navigator` and the other for `Microsoft Internet Explorer`. Then w3c introduced web standards, and browsers implemented them, but the legacy website support should also be there. So, in order to handle this, browser's keep 3 modes in them typically.

#### 1. Quirks mode
Support for legacy web pages is given. This is done for backward compatibility.

#### 2. No Quirks mode
This is the mode browsers should be using by default, unless instructed otherwise. It should support the latest web standards as specified by W3C.

#### 3. Limited Quirks mode
Supports some of the legacy features.

So, when the browser receives a document, it needs to know which mode to parse the HTML in. This is where the doctype declaration comes in. 

```
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Hello World!</title>
  </head>
  <body></body>
</html>
```

The above doctype declaration would trigger the `No Quirks` mode. Prior to HTML5, there were complicated doctype declarations. When the browser would see it, either the `Limited Quirks mode` or `Quirks mode` would get activated. That is the only use of doctype declarations, to tell browser in which mode to parse the document