---
title: "Exceptionally"
date: 2012-09-14T12:00:00Z
draft: true
sidebar: false
tags: ["grails","development"]
preview: "_preview.jpg"
hero: ""
summary: ""
---

Trying to come up with a strategy for [handling errors and exceptions](http://mrhaki.blogspot.nl/2009/09/groovy-goodness-exception-handling.html), we came across some [interesting discussions](http://forum.springsource.org/showthread.php?68285-Service-Layer-Exceptions) and/or Holy Wars.  
I'll try to elaborate a bit on my thoughts and the strategy that was decided for the plugin. 

## Keeping under Wraps
First of all the purpose of the Glickr plugin (or any plugin the implements some interface I guess) is to make the translation of the [native language constructs](http://groovy.codehaus.org/Scripts+and+Classes) and classes (objects) to the particular API and vice versa.

Ideally, the user of the plugin should not be bothered with the specification or workings of the Flickr API at all. Furthermore, the user of the plugin will actually be a programmer creating an application that will or will not have a [humanoid](http://en.wikipedia.org/wiki/Humanoid) working with it. How this application deals with errors and exceptions should not be up to me (the developer of the API) but up to my user (the programmer of the application).
So I should keep as much under wraps as possible, but not too much. Still with me? 

To make the rest of this post easier to read, let's agree on the 4 different actors [layered](https://3.bp.blogspot.com/-R554d4PYmKI/T9cLHkCrhmI/AAAAAAAAFNM/oTWUY1g-nHQ/s1600/Stack+Of+People+And+Chairs.jpg) on top of each other in our scenario; 
- **Human**; i.e. the user of an application using the plugin. Might or might not be applicable in every scenario
- **Programmer**; i.e. a software developer implementing an application using the plugin (_Programmer != Human, we all know that_)
- **Me**; i.e. He that Has to Hide the API details
- **API**; i.e. the [Flick API](http://www.flickr.com/services/api/), which is beyond the control of the other three actors and reportedly constructed in a presumably nice and happening office somewhere downtown San Francisco

## To Err is Human
According to a dictionary, a _Recoverable Error_ is "_'an error that does not prevent program execution'_" which is interpreted by me as "_'not meeting the business rules'_", which are in this case, some rules of the Flickr API, like _'at least 1 result should match your search criteria'_.
Real world business rules of an application are beyond the scope of the plugin.

#### Example:
A **Human** or **Programmer** searches for _[Obi-Wan Kenobi](http://en.wikipedia.org/wiki/Obi-Wan_Kenobi)_ in the _[Star Trek](http://en.wikipedia.org/wiki/Star_Trek)_ database.  
Result? Not found, but a recoverable error (search for [another person](http://en.wikipedia.org/wiki/Spock) or in [another database](http://en.wikipedia.org/wiki/Star_Wars)).  
An Error but not an Exception.

**Humans** can make Errors, but it is up to the **Programmer** to decide how to interact with the **Human** about this unfortunate situation (if there is a **Human** involved at all, think good old-fashioned batch programs).  
We still agree it's an Recoverable Error not an [Exception](http://groovy.codehaus.org/JN3035-Exceptions), don't we?

#### Next Example:
The **API** could report back to **Me** that the "Service is temporary not available".  
While this does give **Me** a hint that this error could be recoverable, it is very hard for **Me** to deal with with the underlying problem.  
The (help-desk of the) **Programmer** might figure out when Flickr finishes their backup of [7 billion images](http://blog.flickr.net/en/2012/04/25/say-hello-to-the-new-flickr-uploadr/) or if there was a hostile takeover by [Buy N Large](http://pixar.wikia.com/Buy_N_Large), but that's as close to recovery we could get.

The **API** will respond this _Recoverable Error_ every now and then, but neither **Me** nor a **Human** could actually deal with the possible recovery (such as: when and/or how often to retry). 

## Exceptional Behaviour
We've dealt with the **Human** and the **API** so far, they both are allowed to make errors, and we can not blame 'em for it. What's left to deal with are errors that are introduced by one of the other two actors.
As the developer of the plugin I do not know who the **Programmer** will be, so I need to provide her/him/they with the information needed to blame **Me** for the error that should be solved in the plugin and will friendly inform her of errors that she can solve herself (syntax problems mostly, specially since the interface will probably not be 100% [type-safe](http://en.wikipedia.org/wiki/Type_safety) and will use plenty of [late-binding](http://en.wikipedia.org/wiki/Late_binding)). 

To prevent error handling code from messin' up the undoubtedly beautiful code produced by the **Programmer** I will be throwing Groovy [Exceptions](http://en.wikipedia.org/wiki/Exception_handling) where applicable. Here's what I decided to implement for the different types of errors we've just elaborated on; 
- **Not meeting the business rules**, which does not prevent program execution and therefor won't produce a Groovy Exception, but will return a NULL rather than the suspected object
- **Recoverable API situations** will be throwing a FlickrServiceApiException
- **Errors that could be solved by the Programmer** will be throwing a FlickrServiceSyntaxException
- **All other problems** messing up program execution (but can only be solved by the developer of the plugin) will be throwing a FlickrServicePluginException

This should enable the programmer to write code that just checks for business logic (is there an object returned or a NULL value) and catch FlickrServiceException (all three flavours will inherit from it) at a more sensible place in the application. Last but not least, while the thrown Exception will include detailed technical information about the actual source of the problem, one should never, and I do mean NEVER, bother a [normal human being](http://www.joelonsoftware.com/uibook/chapters/fog0000000062.html) with this cryptical programming stuff. Promised?