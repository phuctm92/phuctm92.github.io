---
title: "Async and defer in script HTML tag"
date: 2022-09-09 18:00:00 +0700
categories: [Programming]
tags: [HTML, Javascript, Performance]

---
**Async** and **defer** are two of the attributes of script tags in html. Both properties are used to specify that the javascript content is downloaded **at the same time as the page rendering (asynchronously)**. However, these two properties will work differently.
<!--more-->
![enter image description here](https://i.stack.imgur.com/pI1Wn.png)
*Image source: Internet*
## 1. Script without attribute
- HTML is stopped to parse when it hit the script file
- Fetch the script file
- Execute the script before parsing is resumed.

## 2. Async
- Download the script during the HTML is parsing **(same as defer)**
- **Interrupt** the HTML parser to execute the script when it has finished downloaded completely.
- **Execute as soon as possible** (before parsing completes, in no particular order)

## 3. Defer
- Download the script during the HTML is parsing **(same as async)**
- **Not interrupt** the HTML parser to execute
- **Only** execute the script after the parser has completed (before the [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/API/Window/DOMContentLoaded_event) event)

****Note***: It seems to be that the effect of **defer** is similar to **script without attribute** if the script is put at the bottom of HTML (before the closing `</body>` tag). So, let's try to put **defer** in the `<head>` tag to be downloaded sooner.

## 4. When should I use what?
Typically you want to use **async** where possible, then defer then no attribute. Here are some general rules to follow:

-   If the script is modular and does not rely on any scripts then use async.
-   If the script relies upon or is relied upon by another script then use defer.
-   If the script is small and is relied upon by an async script then use an inline script with no attributes placed above the async scripts.

## 5. Reference
1. [https://pagespeedchecklist.com/async-and-defer](https://pagespeedchecklist.com/async-and-defer){:target="_blank"}
2. [https://www.linkedin.com/pulse/async-vs-defer-attributes-javascript-diwaker-mishra/](https://www.linkedin.com/pulse/async-vs-defer-attributes-javascript-diwaker-mishra/){:target="_blank"}

___
*"Success is not final; failure is not fatal: It is the courage to continue that counts." — Winston S. Churchill*{: .text-center.text-success}
