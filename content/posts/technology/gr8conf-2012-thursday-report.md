---
title: "GR8Conf 2012: Torsdag i Danmark"
date: 2012-06-15T12:00:00Z
draft: true
sidebar: false
tags: ["grails","conference"]
preview: ""
hero: ""
summary: ""
---

The first 'official' day of GR8Conf. After some welcome words Groovy project manager Guillaume Laforge took the stage and introduced many new or not so new features of Groovy 1.8 and the upcoming Groovy 2.0. Since this came straight from the source, so you better check out Guillaume's slides.

The Grails Hidden Gems of mrhaki showed us even more of, well hidden gems of Grails, actually. All the examples can be found on github.


A very interesting session by Luke Daley explained a scenario for testing with Geb, which is a browser automation solution, based on Page Object modelling. Of course this did rang many bells. We used to have something similar called TestFrame working for native MS-Windows applications. Such a Page Object based approach will consume quite some development time, but will certainly pay-off in regression tests and/or big applications. Another entry on our todo list.

Without trying to replicate the whole conference, there is still one session I attended on this first day I want to highlight. Andreas Aredal from Sweden plotted the Clean Code mantra of Robert C. Martin, better known as Uncle Bob Martin, on the Grails architecture in the 'Keeping your Grails Code Clean' session.

Some of the Clean Code highlights presented by Andreas:

The MODEL should handle business domain data and it's domain logic
DRY with Named Queries and remember that these are chainable
The VIEW is for presenting data to the user (and only that)
Don't put business logic here and use templates and taglibs for repeating stuff
The CONTROLLER is responsible for handling request flow.
Services should do the heavy lifting and Command Objects should be used if a controller needs data beyond a single domain class.
SERVICES should do the difficult and/of transactional stuff
Thus Services should never store state. Furthermore services are singletons and transactional by default
And JAVASCRIPT should only be responsible for the behavior of your views
Learn jQuery but don't use it for everything and learn Patterns
Oh, and last but not least, not everything is a Grails component, so use plain Groovy or even Java classes when and where appropriate
Quite obvious when summarized like this; but so easy to slip out of our focus in day-to-day coding! Finally Andreas dropped another entry on our todo list; Codenarc for static analysis of Groovy code, like in: put your money where your mouth is.

PS. We sponsor the Devnology podcast that had a nice chat with Uncle Bob Martin

---


<p>The first 'official' day of <a href="http://gr8conf.eu">GR8Conf</a>. After some welcome words Groovy project manager <a href="http://gr8conf.eu/Speakers/Guillaume-Laforge">Guillaume Laforge</a> took the stage and introduced many new or not so new features of Groovy 1.8 and the upcoming Groovy 2.0. Since this came straight from the source, so you better check out <a href="http://www.slideshare.net/glaforge/groovy-18-and-20-at-gr8conf-europe-2012">Guillaume's slides</a>.
</p><p>The <a href="http://gr8conf.eu/Presentations/Grails-hidden-Gems">Grails Hidden Gems</a> of <a href="http://gr8conf.eu/Speakers/MrHaKi">mrhaki</a> showed us even more of, well hidden gems of Grails, actually. All the examples can be found on <a href="https://github.com/mrhaki/gr8conf2012-grails-hidden-gems">github</a>.</p>
<img border="0" height="150" src="http://3.bp.blogspot.com/-j0gKDzZoe_w/T9tzqLsFc9I/AAAAAAAAAO8/YhpUAn28Lr0/s200/556574_407903282581832_1683816066_n.jpg" style="clear: left; float: left; margin-bottom: 1em; margin-right: 1em;" width="200" /><p>A very interesting session by <a href="http://gr8conf.eu/Speakers/Luke-Daley">Luke Daley</a> explained a scenario for testing with <a href="http://www.gebish.org/">Geb</a>, which is a browser automation solution, based on Page Object modelling. Of course this did rang many bells. We used to have something similar called <a href="http://nl.wikipedia.org/wiki/TestFrame">TestFrame</a> working for native MS-Windows applications. Such a Page Object based approach will consume quite some development time, but will certainly pay-off in regression tests and/or big applications. Another entry on our todo list.</p>
<p>Without trying to replicate the whole conference, there is still one session I attended on this first day I want to highlight. <a href="http://gr8conf.eu/Speakers/Andreas-Aredal">Andreas Aredal</a> from Sweden plotted the Clean Code mantra of Robert C. Martin, better known as <a href="https://twitter.com/#!/unclebobmartin">Uncle Bob Martin</a>, on the Grails architecture in the '<a href="http://gr8conf.eu/Presentations/Keeping-your-Grails-code-clean">Keeping your Grails Code Clean</a>' session.</p>
<p>Some of the Clean Code highlights presented by Andreas:</p>
<ul>
<li>The <b>MODEL</b> should handle business domain data and it's domain logic<br />
<i><a href="http://en.wikipedia.org/wiki/Don't_repeat_yourself">DRY</a> with Named Queries and remember that these are chainable</i></li>
<li>The <b>VIEW</b> is for presenting data to the user (and only that)<br />
<i>Don't put business logic here and use templates and taglibs for repeating stuff</i>
</li>
<li>The <b>CONTROLLER</b> is responsible for handling request flow<b>.</b><br />
<i>Services should do the heavy lifting and Command Objects should be used if a controller needs data beyond a single domain class.</i>
</li>
<li><b>SERVICES</b> should do the difficult and/of transactional stuff<br />
<i>Thus Services should never store state. Furthermore services are singletons and transactional by default</i>
</li><li>And <b>JAVASCRIPT</b> should only be responsible for the behavior of your views<br />
<i>Learn jQuery but don't use it for everything and learn Patterns</i></li>
<li>Oh, and last but not least, not everything is a Grails component, so use plain Groovy or even Java classes when and where appropriate</li>
</ul>
<p>Quite obvious when summarized like this; but so easy to slip out of our focus in day-to-day coding! Finally Andreas dropped another entry on our todo list; <a href="http://codenarc.sourceforge.net/">Codenarc</a> for static analysis of Groovy code, like in: put your money where your mouth is.</p>
<p>PS. We sponsor the Devnology podcast that had a <a href="http://devnology.nl/podcast/10-content/98-devnology-podcast-006">nice chat with Uncle Bob Martin</a></p><p></p>
