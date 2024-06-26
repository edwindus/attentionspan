---
title: "Fun Project taking shape"
date: 2014-12-14T12:00:00Z
draft: false
sidebar: false
tags: ["Jokers Wild Tribute"]
preview: "_preview.jpg"
hero: "_hero.jpg"
summary: "Introduction of the Jokers Wild slotmachine and deciding on an approach to build a tribute"
---

A couple of months ago I came across this nice [kickstarter initiative](https://www.kickstarter.com/projects/alexklein/kano-a-computer-anyone-can-make) called [Kano](http://www.kano.me/). Well over 13 thousand people backend them up; and they collected 15 times the 100K dollar they needed to kickstart their product. Well Done!

We just had to [order one](https://www.youtube.com/watch?v=O9aZ8rVi7Bg) trying to deepen my son interest in computer(game)s somewhat using the fun [Kano Blocks](https://www.youtube.com/watch?v=AuqRGEXznfQ) environment to learn about programming using [Minecraft](http://en.wikipedia.org/wiki/Minecraft) as an excellent instrument to teach the logic of coding and 3D encoding.

![Kano raised over $1 million on kickstarter, from nearly 12,000 backers including Apple co-founder Steve Wozniak](kano-001.jpg)
![The whole kit assembled plugs into a standard HDMI port and wireless Bluetooth keyboard](kano-002.jpg)

Kano is built on a [Raspberry Pi](http://en.wikipedia.org/wiki/Raspberry_Pi) single-board computer running a heavily modified linux-distribution.

Before switching to a Bachelor degree in [Computer Science](http://en.wikipedia.org/wiki/Computer_science), I studied [Electronics](http://en.wikipedia.org/wiki/Electronics) at the K.M.T.S. in Utrecht. Something in playing with this Kano computer (re)sparked my interest in some electronics.

![A tool to test electronical components, build by yours truly while at KMTS highschool in 1987](kmts.jpg)
![Arduino is an open-source single-board micro-controllor](arduino.jpg)

But a Raspberry Pi is still a complete computer and I was looking for something more hands-on, and remember that I read a lot about [Arduino's](http://www.arduino.cc/) in [MAKE magazine](http://makezine.com/) in the past few years. The Arduino seems to be a perfect toy for a fun project. All I needed now was an idea.

And at sometime during the new few days an idea seemed to fall in place:  
_What if I tried to make a simple [slotmachine](http://en.wikipedia.org/wiki/Slot_machine) using an Arduino?_

That would need to have a lot of different components; like running [stepper motors](http://en.wikipedia.org/wiki/Stepper_motor) to drive the reels, trying [charlieplexing](http://en.wikipedia.org/wiki/Charlieplexing) as a simple way of multiplexing approximately 10 different buttons to the limited pins of the Arduino and using a [Serial Pheriperal Interface](http://arduino.cc/en/Reference/SPI) to drive approximately 100 different [LED's](http://en.wikipedia.org/wiki/Light-emitting_diode) for the display with the very limited input pins.
If this was not going to provide enough of a challenge, what else would?

![An image of the original Jokers Wild slotmachine (obviously) found at a website called GokkastenArchief.nl](gokkasten-archief-nl-001.jpg)
![Another image found online of the original display for sale, unfortunaly no longer available](hud.jpg)

When I was 17, studying Electronics, there was one particular fruitmachine I liked to play. That particular machine, called [_Jokers Wild_](https://www.gokkastenarchief.nl/online/jokers-wild/), and it's gameplay will be my example in building a tribute fruitmachine based on an Arduino. 

That should be fun, shouldn't it?