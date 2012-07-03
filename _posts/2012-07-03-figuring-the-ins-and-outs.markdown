---
layout: post
title: Figuring the ins and outs
published: false
---

Based on the [previous decision about how the words will be arranged]({{ site.baseurl}}/2012/06/26/laying-out-the-words.html),
I can see that there are a total of twenty words which need to be illuminated. This post is about the ways that this can be
done, and the pros and cons of the approaches.

## Twenty I/Os
Yup, it's gotta be the most obvious approach I could take. It's pretty simple to understand and actually does have a good point or two, regardless of the downsides.

![Schematic for Twenty I/Os]({{ site.baseurl }}/images/2012-07-03-twenty-ios-schematic.png)

#### Pros
 * Easy to handle higher power loads through a transistor
 * Can illuminate any number of LEDs concurrently

#### Cons
 * Requires a silly number of I/O pins on the µC

## Shift Registers
A common way of expanding available parallel I/O pins.

![Schematic for Shift Registers]({{ site.baseurl }}/images/2012-07-03-shift-registers-schematic.png)

#### Pros
 * Easy to handle higher power loads through a transistor
 * Can illuminate any number of LEDs concurrently

#### Cons
 * For twenty I/O I'd likely need three 8bit devices, which all adds to the cost.
   While cost is not a primary factor in doing this little exercise, it seems likely that add
   three devices is going to be more expensive, and more complicated, than simply getting a bigger µC

## Multiplexing
This involves arranging the LEDs in a grid, in this case 5x4, and arranging the state of the I/O pins of the µC
such that current may flow through a _particular_ LED.

![Schematic for Multiplexing]({{ site.baseurl }}/images/2012-07-03-multiplexing-schematic.png)

#### Pros
 * Reduced number of I/O pins required on the µC, 9 in this case
 * Possible to handle higher power loads through transistors

#### Cons
 * More complicated (impossible?) to illuminate arbitrary sets of LEDs concurrently

## Charlieplexing
This involves making use of the tristate nature of the µC I/O pins, where a pin configured as an input is high impedance. Allows individual addressing of twenty LEDs using only five I/O pins.

![Schematic for Charlieplexing]({{ site.baseurl }}/images/2012-07-03-charlieplexing-schematic.png)

#### Pros
 * Reduced number of I/O pins on the µC, 5 in this case

#### Cons
 * Difficult to provide power beyond that allowed by the µC, typically 25mA
 
   Because the arrangement involves current flowing between two output pins it's not really simple, from what I've been able to see,
   to introduce higher current loads. It may be possible with some incantation of diodes and transistors, but I'm not hopeful, and
   I've not seen any examples of such online.
 
 * Not possible to illuminate multiple LEDs concurrently in any sensible fashion
