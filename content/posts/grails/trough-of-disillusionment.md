---
title: "Trough of Disillusionment"
date: 2012-09-05T12:00:00Z
draft: true
sidebar: false
tags: ["grails","development"]
preview: ""
hero: ""
summary: ""
---

In the first weeks after GR8Conf I enthusiastically started with the blog and development of the plugin. Sadly we had to deal with an event in real life that thoroughly consumed all our energy and enthusiasm.

While the last mumbling on this blog is already a couple of months away, today seems like a good day to drop some thoughts on the internets. On a positive note I could argue I'm perfectly compliant with the Gartner Hype Cycle, so nothing is lost while I commence the Slope of Enlightenment.
REST assured

With slightly over 200 interface methods, the Flickr API is quite an impressive beast to tame. What I aim to achieve (given I'll arrive somewhere mimicking the Plateau of Productivity), is a full implementation of the API as a Grails service, using native (and probably extensive) Groovy classes for the relevant entities, like Photos, People, Places, etcetera. The REST format seems to be the most sensible way to approach the API, so essentially I'll be implementing a Facade for the REST.request and corresponding XML response.
private def apiCall

After some tire kicking I started with an abstraction of what all API calls should do:
Validate the parameters before doing the call to Flickr
Well eh, do the actual call
Process the response or handle any errors
In Pseudo Groovy Code it looks something like this:
void apiCall(method, params) {
   if (validator(params)) {
      try {
         def rsp = doApiCall(method,params)
         return process(rsp)
      } catch (Exception ex) {
         ...
      }
   } else {
      // todo: raise validation exception
   }
}
Non disclosure

Now using the power of Groovy Closures I made the params, the validator and the processor variable for each different API method. Furthermore, to help in the maintenance of what will potentially be over 200 different sets of params, validators and processors, I decided to wrap the Closures in a Class. The whole concept will likely evolve over time, but generally the code looks like this:
//
//  abstracting the whole call handling with closures implemented in individual classes and connected below
//
private def apiCall(def apiImplementation, def apiModel = {} ) {
    def validator = apiImplementation.validatorClosure
    def params    = apiImplementation.paramsClosure
    def processor = apiImplementation.processorClosure

    if (validator(apiModel())) {
        try {
            def rsp = doApiCall(apiImplementation.apiMethod, params(apiModel()))
            return processor(rsp,apiModel())
        } catch (FlickrException ex) {
            FlickrExceptionHandler.handleApiCallException(ex)
        }
    }
    // todo: raise validation exception
    return apiModel()
}
Now the definition of a single Facade method looks like this:
FlickrPhoto photosGetInfo(FlickrPhoto photo) {
    return apiCall(
        new org.glickr.api.photos.photosGetInfo(),
        { photo }) as FlickrPhoto
}
And the actual implementation of the Flickr API method is done in this class:
class photosGetInfo implements FlickrApiMethod{
    static final String apiMethod = 'flickr.photos.getInfo'

    Closure validatorClosure = { FlickrPhoto photo ->
        if (!photo || photo?.id <= 0) { return false } // missing model
        return true
    }

    Closure paramsClosure = { FlickrPhoto photo ->
        [photo_id:photo?.id, secret:(photo?.secret ?:'')]
    }

    Closure processorClosure = { GPathResult response, FlickrPhoto photo ->
        photo.title       = response.photo.title.toString()
        photo.description = response.photo.description.toString()
        photo.isPublic    = (response.photo.visibility.@ispublic?.toString() == '1')
        // etcetera              
        
        return photo
    }
}
That'll be it for today. Any ideas, suggestions or blatant criticism will be greatly appreciated while I code my way up the Slope of Enlightenment towards an initial alfa release of the Glickr plugin.


------


In the first weeks after <a href="http://gr8conf.eu/">GR8Conf</a> I enthusiastically started with the blog and development of the plugin. Sadly we had to deal with an event in real life that thoroughly consumed all our energy and enthusiasm. <div class="separator" style="clear: both; text-align: center;">
<a href="http://3.bp.blogspot.com/-3H9x3dr-cCo/UEcGsSa8wsI/AAAAAAAAAP4/mcqQS67yS9s/s1600/gartner-hype-cycle.png" style="clear: right; float: right; margin-bottom: 1em; margin-left: 1em;"><img border="0" height="130" src="http://3.bp.blogspot.com/-3H9x3dr-cCo/UEcGsSa8wsI/AAAAAAAAAP4/mcqQS67yS9s/s200/gartner-hype-cycle.png" width="200" /></a></div>
While the last mumbling on this blog is already a couple of months away, today seems like a good day to drop some thoughts on the <a href="http://en.wikipedia.org/wiki/Internets">internets</a>. On a positive note I could argue I'm perfectly compliant with the Gartner <a href="http://en.wikipedia.org/wiki/Hype_cycle">Hype Cycle</a>, so nothing is lost while I commence the Slope of Enlightenment.
<h5>REST assured</h5>
With slightly over 200 interface methods, the <a href="http://www.flickr.com/services/api/">Flickr API</a> is quite an impressive beast to tame. What I aim to achieve (given I'll arrive somewhere mimicking the <a href="http://en.wikipedia.org/wiki/Hype_cycle">Plateau of Productivity</a>), is a full implementation of the API as a Grails service, using native (and probably extensive) Groovy classes for the relevant entities, like Photos, People, Places, etcetera.
The <a href="http://www.flickr.com/services/api/request.rest.html">REST format</a> seems to be the most sensible way to approach the API, so essentially I'll be implementing a <a href="http://en.wikipedia.org/wiki/Design_Patterns_(book)">Facade</a> for the REST.request and corresponding <a href="http://www.flickr.com/services/api/response.rest.html">XML response</a>.
<h5>private def apiCall</h5>
After some <a href="http://www.urbandictionary.com/define.php?term=tire+kicker">tire kicking</a> I started with an abstraction of what all API calls should do:
<ol>
<li>Validate the parameters before doing the call to Flickr</li>
<li>Well eh, do the actual call</li>
<li>Process the response or handle any errors</li>
</ol>
In Pseudo Groovy Code it looks something like this:
<pre class="brush: groovy;">void apiCall(method, params) {
   if (validator(params)) {
      try {
         def rsp = doApiCall(method,params)
         return process(rsp)
      } catch (Exception ex) {
         ...
      }
   } else {
      // todo: raise validation exception
   }
}
</pre>

<h5>Non disclosure</h5>
Now using the power of <a href="http://groovy.codehaus.org/Closures">Groovy Closures</a> I made the params, the validator and the processor variable for each different API method. Furthermore, to help in the maintenance of what will potentially be over 200 different sets of params, validators and processors, I decided to wrap the Closures in a Class. The whole concept will likely evolve over time, but generally the code looks like this:


<pre class="brush: groovy;">//
//  abstracting the whole call handling with closures implemented in individual classes and connected below
//
private def apiCall(def apiImplementation, def apiModel = {} ) {
    def validator = apiImplementation.validatorClosure
    def params    = apiImplementation.paramsClosure
    def processor = apiImplementation.processorClosure

    if (validator(apiModel())) {
        try {
            def rsp = doApiCall(apiImplementation.apiMethod, params(apiModel()))
            return processor(rsp,apiModel())
        } catch (FlickrException ex) {
            FlickrExceptionHandler.handleApiCallException(ex)
        }
    }
    // todo: raise validation exception
    return apiModel()
}
</pre>

Now the definition of a single Facade method looks like this:

<pre class="brush: groovy;">FlickrPhoto photosGetInfo(FlickrPhoto photo) {
    return apiCall(
        new org.glickr.api.photos.photosGetInfo(),
        { photo }) as FlickrPhoto
}
</pre>

And the actual implementation of the Flickr API method is done in this class:

<pre class="brush: groovy;">class photosGetInfo implements FlickrApiMethod{
    static final String apiMethod = 'flickr.photos.getInfo'

    Closure validatorClosure = { FlickrPhoto photo -&gt;
        if (!photo || photo?.id &lt;= 0) { return false } // missing model
        return true
    }

    Closure paramsClosure = { FlickrPhoto photo -&gt;
        [photo_id:photo?.id, secret:(photo?.secret ?:'')]
    }

    Closure processorClosure = { GPathResult response, FlickrPhoto photo -&gt;
        photo.title       = response.photo.title.toString()
        photo.description = response.photo.description.toString()
        photo.isPublic    = (response.photo.visibility.@ispublic?.toString() == '1')
        // etcetera              
        
        return photo
    }
}
</pre>

That'll be it for today. Any ideas, suggestions or blatant criticism will be greatly appreciated while I code my way up the <a href="http://en.wikipedia.org/wiki/Hype_cycle">Slope of Enlightenment</a> towards an initial alfa release of the Glickr plugin.


 


