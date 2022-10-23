---
title: "Exceptionally"
date: 2012-09-14T12:00:00Z
draft: true
sidebar: false
tags: ["grails","development"]
preview: ""
hero: ""
summary: ""
---



Trying to come up with a strategy for handling errors and exceptions, we came across some interesting discussions and/or Holy Wars. I'll try to elaborate a bit on my thoughts and the strategy that was decided for the plugin. 

Keeping under Wraps

First of all the purpose of the Glickr plugin (or any plugin the implements some interface I guess) is to make the translation of the native language constructs and classes (objects) to the particular API and vice versa.


Ideally, the user of the plugin should not be bothered with the specification or workings of the Flickr API at all. Furthermore, the user of the plugin will actually be a programmer creating an application that will or will not have a humanoid working with it. How this application deals with errors and exceptions should not be up to me (the developer of the API) but up to my user (the programmer of the application).
So I should keep as much under wraps as possible, but not too much. Still with me? 

To make the rest of this post easier to read, let's agree on the 4 different actors layered on top of each other in our scenario; 
Human; i.e. the user of an application using the plugin. Might or might not be applicable in every scenario
Programmer; i.e. a software developer implementing an application using the plugin (Programmer != Human, we all know that)
Me; i.e. He that Has to Hide the API details
API; i.e. the Flick API, which is beyond the control of the other three actors and reportedly constructed in a presumably nice and happening office somewhere downtown San Francisco

To Err is Human

According to a dictionary, a 'Recoverable Error' is "an error that does not prevent program execution" which is interpreted by me as "not meeting the business rules", which are in this case, some rules of the Flickr API, like "at least 1 result should match your search criteria".
Real world business rules of an application are beyond the scope of the plugin.

Example:
A Human or Programmer searches for "Obi-Wan Kenobi" in the Star Trek database. Result? Not found, but a recoverable error (search for another person or in another database). An Error but not an Exception.
Humans can make Errors, but it is up to the Programmer to decide how to interact with the Human about this unfortunate situation (if there is a Human involved at all, think good old-fashioned batch programs).
We still agree it's an Recoverable Error not an Exception, don't we?

Next Example:
The API could report back to Me that the "Service is temporary not available".
While this does give Me a hint that this error could be recoverable, it is very hard for Me to deal with with the underlying problem. The (help-desk of the) Programmer might figure out when Flickr finishes their backup of 7 billion images or if there was a hostile takeover by Buy N Large, but that's as close to recovery we could get.
The API will respond this Recoverable Error every now and then, but neither Me nor a Human could actually deal with the possible recovery (such as: when and/or how often to retry). 

Exceptional Behaviour

We've dealt with the Human and the API so far, they both are allowed to make errors, and we can not blame 'em for it. What's left to deal with are errors that are introduced by one of the other two actors.
As the developer of the plugin I do not know who the Programmer will be, so I need to provide her/him with the information needed to blame Me for the error that should be solved in the plugin and will friendly inform her of errors that she can solve herself (syntax problems mostly, specially since the interface will probably not be 100% type-safe and will use plenty of late-binding). 

To prevent error handling code from messin' up the undoubtedly beautiful code produced by the Programmer I will be throwing Groovy Exceptions where applicable. Here's what I decided to implement for the different types of errors we've just elaborated on; 
Not meeting the business rules, which does not prevent program execution and therefor won't produce a Groovy Exception, but will return a NULL rather than the suspected object
Recoverable API situations will be throwing a FlickrServiceApiException
Errors that could be solved by the Programmer will be throwing a FlickrServiceSyntaxException
All other problems messing up program execution (but can only be solved by the developer of the plugin) will be throwing a FlickrServicePluginException

This should enable the programmer to write code that just checks for business logic (is there an object returned or a NULL value) and catch FlickrServiceException (all three flavours will inherit from it) at a more sensible place in the application. Last but not least, while the thrown Exception will include detailed technical information about the actual source of the problem, one should never, and I do mean NEVER, bother a normal human being with this cryptical programming stuff. Promised?

----

Trying to come up with a strategy for <a href="http://mrhaki.blogspot.nl/2009/09/groovy-goodness-exception-handling.html" target="_blank">handling errors and exceptions</a>, we came across <a href="http://forum.springsource.org/showthread.php?68285-Service-Layer-Exceptions" target="_blank">some interesting discussions</a> and/or Holy Wars. I'll try to elaborate a bit on my thoughts and the strategy that was decided for the plugin.
<br />
<br />
<h4>
Keeping under Wraps</h4>
First of all the purpose of the Glickr plugin (or any plugin the implements some interface I guess) is to make the translation of the <a href="http://groovy.codehaus.org/Scripts+and+Classes" target="_blank">native language constructs</a> and classes (objects) to the particular API and vice versa.<br />
<br />
<div class="separator" style="clear: both; text-align: center;">
<a href="http://2.bp.blogspot.com/-FWshV4hzrNU/UFGEiqs4qZI/AAAAAAAAARU/H-C5pup0tbw/s1600/error2.gif" imageanchor="1" style="clear: left; float: left; margin-bottom: 1em; margin-right: 1em;"><img border="0" height="178" src="http://2.bp.blogspot.com/-FWshV4hzrNU/UFGEiqs4qZI/AAAAAAAAARU/H-C5pup0tbw/s200/error2.gif" width="200" /></a></div>
Ideally, the user of the plugin should not be bothered with the specification or workings of the Flickr API at all.
Furthermore, the user of the plugin will actually be a programmer creating an application that will or will not have a <a href="http://en.wikipedia.org/wiki/Humanoid" target="_blank">humanoid</a> working with it. How this application deals with errors and exceptions should not be up to me (the developer of the API) but up to my user (the programmer of the application).<br />
So I should keep as much under wraps as possible, but not too much. Still with me?
<br />
<br />
To make the rest of this post easier to read, let's agree on the 4 different actors <a href="http://3.bp.blogspot.com/-R554d4PYmKI/T9cLHkCrhmI/AAAAAAAAFNM/oTWUY1g-nHQ/s1600/Stack+Of+People+And+Chairs.jpg" target="_blank">layered</a> on top of each other in our scenario;
<br />
<ul>
<li><strong><span style="color: #666666;">Human</span></strong>; i.e. the user of an application using the plugin. Might or might not be applicable in every scenario</li>
<li><strong><span style="color: #666666;">Programmer</span></strong>; i.e. a software developer implementing an application using the plugin <i>(Programmer != Human, we all know that)</i></li>
<li><strong><span style="color: #666666;">Me</span></strong>; i.e. He that Has to Hide the API details</li>
<li><strong><span style="color: #666666;">API</span></strong>; i.e. the <a href="http://www.flickr.com/services/api/" target="_blank">Flick API</a>, which is beyond the control of the other three actors and reportedly constructed in a presumably nice and happening office somewhere downtown San Francisco
</li>
</ul>
<br />
<h4>
To Err is Human</h4>
According to <i>a</i> dictionary, a 'Recoverable Error' is "an error that does not prevent program execution" which is interpreted by me as "not meeting the business rules", which are in this case, some rules of the Flickr API, like <i>"at least 1 result should match your search criteria"</i>.<br />
Real world business rules of an application are beyond the scope of the plugin.<br />
<br />
Example:<br />
A <b><span style="color: #666666;">Human</span></b> or <b><span style="color: #666666;">Programmer</span></b> searches for "<a href="http://en.wikipedia.org/wiki/Obi-Wan_Kenobi" target="_blank">Obi-Wan Kenobi</a>" in the <a href="http://en.wikipedia.org/wiki/Star_Trek" target="_blank">Star Trek</a> database. Result? Not found, but a recoverable error (search for <a href="http://en.wikipedia.org/wiki/Spock" target="_blank">another person</a> or in <a href="http://en.wikipedia.org/wiki/Star_Wars" target="_blank">another database</a>).&nbsp;An Error but not an Exception.<br />
<b><span style="color: #666666;">Humans</span></b> can make Errors, but it is up to the <b><span style="color: #666666;">Programmer</span></b> to decide how to interact with the <b><span style="color: #666666;">Human</span></b> about this unfortunate situation (if there is a Human involved at all, think good old-fashioned batch programs).<br />
We still agree it's an Recoverable Error not an <a href="http://groovy.codehaus.org/JN3035-Exceptions" target="_blank">Exception</a>, don't we?<br />
<br />
Next Example:<br />
The <strong><span style="color: #666666;">API</span></strong> could report back to <strong><span style="color: #666666;">Me</span></strong> that the "Service is temporary not available".<br />
While this does give <strong><span style="color: #666666;">Me</span></strong> a hint that this error <i>could</i> be recoverable, it is very hard for <strong><span style="color: #666666;">Me</span></strong> to deal with with the underlying problem. The (help-desk of the)&nbsp;<strong><span style="color: #666666;">Programmer</span></strong> might figure out when Flickr finishes their backup of <a href="http://blog.flickr.net/en/2012/04/25/say-hello-to-the-new-flickr-uploadr/" target="_blank">7 billion images</a> or if there was a hostile takeover by <a href="http://pixar.wikia.com/Buy_N_Large" target="_blank">Buy N Large</a>, but that's as close to recovery we could get.<br />
The <strong><span style="color: #666666;">API</span></strong> will respond this Recoverable Error every now and then, but neither&nbsp;<strong><span style="color: #666666;">Me</span></strong> nor a <strong><span style="color: #666666;">Human</span></strong> could actually deal with the possible recovery (such as: when and/or how often to retry).
<br />
<br />
<h4>
Exceptional Behaviour</h4>
We've dealt with the <strong><span style="color: #666666;">Human</span></strong> and the <strong><span style="color: #666666;">API</span></strong> so far, they both are allowed to make errors, and we can not blame 'em for it. What's left to deal with are errors that are introduced by one of the other two actors.<br />
As the developer of the plugin I do not know who the <strong><span style="color: #666666;">Programmer</span></strong> will be, so I need to provide <a href="http://watermarked.cutcaster.com/cutcaster-photo-100042620-Nerdy-Girl.jpg" target="_blank">her</a>/him with the information needed to blame <strong><span style="color: #666666;">Me</span></strong> for the error that should be solved in the plugin and will friendly inform her of errors that she can solve herself (syntax problems mostly, specially since the interface will probably not be 100% <a href="http://en.wikipedia.org/wiki/Type_safety" target="_blank">type-safe</a>&nbsp;and will use plenty of <a href="http://en.wikipedia.org/wiki/Late_binding" target="_blank">late-binding</a>).
<br />
<br />
To prevent error handling code from messin' up the undoubtedly beautiful code produced by the <b><span style="color: #666666;">Programmer</span></b> I will be throwing Groovy <a href="http://en.wikipedia.org/wiki/Exception_handling" target="_blank">Exceptions</a> where applicable. Here's what I decided to implement for the different types of errors we've just elaborated on;
<br />
<ul>
<li><strong>Not meeting the business rules</strong>, which does not prevent program execution and therefor won't produce a Groovy Exception, but will return a <i>NULL</i> rather than the suspected object</li>
<li><strong>Recoverable API situations</strong> will be throwing a FlickrServiceApiException</li>
<li><strong>Errors that could be solved by the Programmer</strong> will be throwing a FlickrServiceSyntaxException</li>
<li><strong>All other problems</strong> messing up program execution (but can only be solved by the developer of the plugin) will be throwing a FlickrServicePluginException</li>
</ul>
<br />
This should enable the programmer to write code that just checks for business logic (is there an object returned or a <i>NULL</i> value) and catch&nbsp;FlickrServiceException&nbsp;(all three flavours will inherit from it) at a more sensible place in the application. Last but not least, while the thrown Exception will include detailed technical information about the actual source of the problem, one should never, and I do mean NEVER, bother a <a href="http://www.joelonsoftware.com/uibook/chapters/fog0000000062.html" target="_blank">normal human being</a> with this cryptical programming stuff. Promised? 
