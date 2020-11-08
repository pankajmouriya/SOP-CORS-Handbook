---
title: Same-Origin Policy - The Core of Web Security
linktitle: Same-Origin Policy
type: book
date: "2019-05-05T00:00:00+01:00"
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---


---------------
**Slides**
  
I am assuming a lot of people here will already know most of the things I will be talking today so to those people, consider it a revision 
------------------


What this chapter will cover ?

* What is the same origin policy?
* Why is it important?
* How does it apply to web

Before understanding or talking about same origin policy, lets ask below questions from ourselves

- Should site A be able to **embed** site B?
- Should site A be able to **link to** site B?
- Should site A be able to **embed** site B and modify its contents?
- Should site A be able to **submit a form** to site B?
- Should site A be able to **embed images** from site B?
- Should site A be able to **embed scripts** from site B?
- Should site A be able to **read data** from site B?

Lets not answer these questions now, we will do some handson exercises and then will answer these questions

## Same Origin Policy
* Fundamental Security of the Web.
* The same-origin policy is a web browser security mechanism that aims to prevent websites from attacking each other **(Portswigger.net)**
* The same-origin policy is a critical security mechanism that restricts how a document or script loaded from one origin can interact with a resource from another origin. It helps isolate potentially malicious documents, reducing possible attack vectors.**(Mozilla Developer Networks)**
* Key thing to remember here is - *Two pages from different sources should not be allowed to interfere with each other*.

Now lets talk about what is an origin?

Look at below URL

{{< figure library="true" src="sop1.png" title="" >}}

{{< figure library="true" src="sop2.png" title="" >}}

Do not worry about all the keywords mentioned inside the URL, we are only concerned for below three keywords

{{< figure library="true" src="sop3.png" title="" >}}

An origin can be defined as a Tuple made of Scheme, Domain and Port. `In another words, "protocol-host-port tuple" is called an "origin". So if two web pages have same scheme(protocol), domain and port then they are both the same origin.`

The following table gives examples of origin comparisons with the URL `http://store.company.com/dir/page.html`

| URL                                             | Outcome     | Reason                                         |
|-------------------------------------------------|-------------|------------------------------------------------|
| http://store.company.com/dir2/other.html        | Same origin | Only the path differs                          |
| http://store.company.com/dir/inner/another.html | Same origin | Only the path differs                          |
| https://store.company.com/page.html             | Failure     | Different protocol                             |
| http://store.company.com:1234/dir/page.html     | Failure     | Different port (http:// is port 80 by default) |
| http://news.company.com/dir/page.html           | Failure     | Different host                                 |

Now that we understand what is an **Origin**, lets understand what a Same Origin Policy is.

Follow slides for better understanding


## Demo

//One Slide About DOM

**DOM** : Document Object Model (DOM)  is a programming interface for HTML and XML documents. In case you are still confused and want to have some more clarity over DOM, you may check this source `https://livedom.lab.xss.academy/` which shows live how DOM looks like. I came across this while doing some google. 


We have two different web applications running in our browser that is `sitea.com` and `siteb.com`

Open both the windows in different tabs in your browser and follow belows instructions. We will be using Browser developer console to do the demos because whatever a JavaScript can do to a website loaded in a browser can also be done in Browser Console.


lets start with the basic command most of us know when we see javascript :)

`alert(1)`

`document.documentURI`

`document.scripts`

`document.body` 

Lets try to access other site resources using this console, but before that lets create a reference variable to open a new window using this window console.

`var bob = window.open('http://sitea.com','right')`

Now that we have a reference defined to `sitea.com`, we can access it. Lets try to access the and see what console shows.

`bob`

`bob.document.body`

Notice that we are able to access the body of bob variable which basically means that we are able to access body of `sitea.com` which we opened in the new window.

if you remember the Same Origin Policy, schema+domain+protocol all match for both the windows we have opened here

window 1 = http://sitea.com
window 2 = http://sitea.com

because it follows the Same Origin Policy, we can access the body of `sitea.com` opened in another tab.

Lets try to open new window but with `siteb.com`

`var bob = window.open('http://siteb.com','right')`

now type `bob.document.body`

Notice the message which says `Permission denied to access property "document" on cross-origin object`. Because it voilates what Same Origin Policy says

window 1 = http:sitea.com
window 2 = http:siteb.com //the domain changes

{{< figure library="true" src="console-sop1.png" title="" >}}

Each tab/window is isolated in browsers

Always remember that each website has its own separate DOM and separate JavaScript environment. 


### Talking about Iframes

* Frames are isolated
* Each iframe has its own separate JavaScript execution environment

#### Demo
Open One website lets say `sitea.com`

Open console

`const iframe = document.createElement('iframe')`

`iframe.src = 'https://siteb.com'`

`document.body.append(iframe)`

`iframe.contentDocument.cookie`

`iframe.contentDoument`
  
`iframe.src = 'http://siteb.com'` //  trying to change the src of iframe

`const res = await fetch('http://sitec.com')`// accessing data cross origin

// find video where we can try toaccess data cross frame kirk jackson

