---
title: "Decide you must"
date: 2012-10-06T12:00:00Z
draft: true
sidebar: false
tags: ["grails","development"]
preview: ""
hero: ""
summary: ""
---

It's inevitable, one day I have to get the plugin out in the open. The whole idea of a plugin is that your code could serve someone else in the community and hence, it should be out there for someone else to find it. But programming is an art as much as it is a science and there's no accounting for taste.
While I do have experience with peer-code-reviews and I do have written numerous little code examples to explain concepts or teach courses, this plugin is something else. And I've been doing tailor-made software for a living, never before did I try to contribute to other tailors.

Pro's

In it's current state, it does have value to other developers wanting to use the Flickr API to get some images and / or users. So that would be a reason to do an "initial public offering" at this point in time. Furthermore, it generally is a good thing to release early and release often. This might give me some feedback about the approach or heaven forbid, my Groovy coding style / knowledge.
The code works for me, but nobody notices that warm feeling (like wetting your pants in a dark suit) and I'm curious to find out if more people are interested in using it, if the approach will work out in the end, if other people can use the exception handling, if they would need more methods or less, if ...

Con's

It's not finished.
No really, I promise. I want to implement way more of the Flickr API, specially the methods that need  authentication are missing badly in the current state.
Also, I'm not a 100% sure if the architecture will hold up once I start implementing more scenario's and methods. And what impact an internal architecture change will have on external users of the plugin.
And I should add regression tests for each and every function. And I ...

Permission you seek?

Finally last night I revisited the instructions in the Grails User Guide, wrote some documentation, read the Release Plugin User Guide and the permission procedure detailed by Yoda Graeme Rocher, bit the bullet and emailed "Seeking permission for initial publication of my Glickr plugin" to the Jedi Grails Developers.
Waiting anxiously for the Force feedback.

-----


<div class="separator" style="clear: right; float: right; margin-bottom: 1em; margin-left: 1em; text-align: center;">
<img border="0" height="200" src="http://4.bp.blogspot.com/-bHYgg73AOz8/UHPtMajCFWI/AAAAAAAAARk/jT-O32Ww-0g/s200/yoda.jpg" width="173" /></div>
It's inevitable, one day I have to get the plugin out in the open. The whole idea of a plugin is that your code could serve someone else in the community and hence, it should be out there for someone else to find it. But programming is an art as much as it is a science and there's <a href="http://en.wiktionary.org/wiki/chacun_%C3%A0_son_go%C3%BBt" target="_blank">no accounting for taste</a>.<br />
While I do have experience with peer-code-reviews and I do have written numerous little code examples to explain concepts or teach courses, this plugin is something else.&nbsp;And I've been doing <a href="http://en.wikipedia.org/wiki/Custom_software" target="_blank">tailor-made software</a> for a living, never before did I try to contribute to other tailors.<br />
<br />
<h4>
Pro's</h4>
In it's current state, it does have value to other developers wanting to use the Flickr API to get some <a href="http://www.flickr.com/services/api/flickr.photos.getInfo.html" target="_blank">images</a> and / or <a href="http://www.flickr.com/services/api/flickr.people.getInfo.html" target="_blank">users</a>. So that would be a reason to do an "<a href="http://en.wikipedia.org/wiki/Pets.com" target="_blank">initial public offering</a>" at this point in time.
Furthermore, it generally is a good thing to <a href="http://en.wikipedia.org/wiki/Release_early,_release_often">release early and release often</a>. This might give me some feedback about the approach or heaven forbid, my Groovy coding style / knowledge.<br />
The code works for me, but nobody notices that warm feeling (like <a href="#" onclick="alert('You do not wanna click this do you?');return false;" title="You don't wanna click this do you?">wetting your pants</a> in a dark suit) and I'm curious to find out if more people are interested in using it, if the approach will work out in the end, if other people can use the exception handling, if they would need more methods or less, if ...<br />
<br />
<h4>
Con's</h4>
<div>
It's not finished.</div>
<div>
No really, I promise. I want to implement way more of the Flickr API, specially the methods that need &nbsp;authentication are missing badly in the current state.</div>
<div>
Also, I'm not a 100% sure if the architecture will hold up once I start implementing more scenario's and methods. And what impact an internal architecture change will have on external users of the plugin.</div>
<div>
And I should add <a href="http://en.wikipedia.org/wiki/Regression_testing" target="_blank">regression tests</a> for each and every function. And I ...</div>
<br />
<h4>
Permission you seek?</h4>
Finally last night I revisited the instructions in the <a href="http://grails.org/doc/latest/guide/plugins.html" target="_blank">Grails User Guide</a>, wrote some <a href="http://www.glickr.org/p/documentation.html" target="_blank">documentation</a>, read the <a href="http://grails-plugins.github.com/grails-release/docs/index.html" target="_blank">Release Plugin User Guide</a> and the <a href="http://grails.org/Creating+Plugins" target="_blank">permission procedure</a> detailed by <strike>Yoda</strike> <a href="http://grails.io/" target="_blank">Graeme Rocher</a>,&nbsp;bit the bullet and emailed "Seeking permission for initial publication of my Glickr plugin" to the <strike>Jedi</strike> <a href="https://twitter.com/grailsframework" target="_blank">Grails Developers</a>.<br />
Waiting anxiously for the Force feedback.