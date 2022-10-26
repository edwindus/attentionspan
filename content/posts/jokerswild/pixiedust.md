---
title: "Pixiedust"
date: 2019-07-06T12:00:00Z
draft: false
sidebar: false
tags: ["Jokers Wild Tribute"]
preview: "_preview.jpg"
hero: "_hero.jpg"
summary: "Counting and categorizing the different sets of lights on the display while testing with a Neopixel strip."
---

Many months have passed, but I found some time to work on the Arduino project again. The objective of the next step is to do a proof of concept on the HUD (head-up display) of the slotmachine. While I have no idea if HUD is the "official" way to refer to the top half of the slotmachine, where the feature-game is played, it seems like a sensible name.

Anyways; the (dutch) website [gokkastenarchief.nl](http://www.gokkastenarchief.nl/online/jokers-wild/) is by far the best reference I could find. The image below shows the "HUD" and what's on there.

![](gokkasten-archief-nl-002.jpg)
![](gokkasten-archief-nl-003.jpg)
![](gokkasten-archief-nl-004.jpg)

The feature-game is triggered by points that are provided by the 4th reel and played with cards that are displayed on this 4th reel too. For now, let's forget about that and just proof the concept of driving all this lights (and some simple sound effects) from the Arduino.

A simple sketch (created with the great online platform [circuits.io](https://www.circuits.io/) by AutoDesk) of the setup used:

![](hud-pov.png)
![](_preview.jpg)

The interesting part is the thing on the bottom-right, called a [NeoPixel](https://www.adafruit.com/products/1376) strip by AdaFruit. I got a leftover piece with 46 NeoPixels that I used to simulate the 3 main parts of the HUD.

1. Display of Points (left) that trigger the feature game (their function is not important for now)
    - Steps **1** through **10**
    - **Mystery Number** alongside position 4
    - **Gelijk is Goed** alongside position 5
    - **Andere Kaart** alongside position 6
    - **Joker** along position 7 and 10
    - **Kaartspel** along position 8,9 and 10
2. Deck of Cards (called **Kaartspel** in dutch) that will start when 8, 9 or 10 points are reached
    - Cards **3** through **10**, **Jack**, **Queen**, **King** and **Ace**
    - Gamble feature **Hoger** (higher) and **Lager** (lower)
3. Prices to win when gambling with the Deck of Cards succeeds
    - 2, 4, 10, 20, 40, 60, 100, 200
    - Special prices **Mystery Prijs**, **Nudges**, **Kies je Prijs** and **Super Match**

![](JokersWild-011.png)
![](JokersWild-013.png)
![](JokersWild-016.png)
![](JokersWild-018.png)

When we count all that up; there are 44 LED's to drive in this proof-of-concept for the HUD. The strip was kept intact and was laid alongside a printout with the symbol.

I thought it was nice to have some simple sound effects to go along with the moving lights, but did not want to use mp3 or such files. Luckily, after some googling I came across this [nice library](https://mycontraption.com/sound-effects-with-and-arduino/) of sound effects that sends simple straightforward signals to a piezo. Little memory footprint and exactly the sort of sound effects I was looking for.


