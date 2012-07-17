---
layout: post
title: Let's get physical
---

## Going from theory to practice
At some point I'm going to have to build this thing, so it's worthwhile to come up with a plan about
exactly what's going to get made. Since this is really just an experiment for me I'd quite like to play
with some new stuff and learn a few new things along the way.

So, without further ado, the plan will be:

 * Desktop model
 * Battery powered
 * Surface mount devices
 * Professionally produced PCB

### Desktop model
It sort of makes sense, at least to me, to make something small enough to handle in the first iteration.
No point making it big, and expensive, if the basics haven't been tested out.

I have some idea for the physical 'enclosure', specifically a bend, engraved acrylic sheet, essentially exposing the
back side of the board behind the front panel. Mounting the board should be pretty straightforward, with spacers or
nylon nuts glued to acrylic and allowing the board to be attached.

I know a _man that can_ handle the engraving of the letters on the plastic, so as long as I pay some attention to the
mounting and general idea in my head when laying out the board, I'm not expecting too many difficulties.

### Battery powered
I'd rather be able to have a clock on a counter or windowsill than requiring it near a power source, like
a wall wart or USB lead. That said, at the moment I'm not too sure what the power requirements will be, and
I'm not really that confident to trust what I might guestimate from datasheets. This will probably, hopefully,
lead me to use overspec'd batteries which have a useful lifetime. I'll have to see.

### Surface mount devices
I've done enough PTH soldering, I'm no demon at it but I know I can and the world has largely moved on. I've
never done SMT soldering, but YouTube suggests the fear factor is the biggest obstacle.

### Professionally produced PCB
I've not made up any PCBs since I was in school and it seems the technology in DIY production hasn't really changed
all that much. You still print the layout, blast the board with UV, develop, etch and cross fingers. Granted it's
been _a while_ since I've gone through the process, but what's new to me is being able to send a shop in China some
files and get some properly made boards back in the post. Gotta try me some of that, especially when it's
[not all that expensive](http://www.seeedstudio.com/depot/fusion-pcb-service-p-835.html).

## Drawing the first line
I know from experience that it's often difficult to decide where to put down the first line on a drawing, or
defining the first API for a piece of software. In some cases it seems that _any_ line will do, within reason,
and putting something down allows me to move on. Clearly the eraser or TipEx comes into play sometimes, but that's
just part of the process.

Given the somewhat vague requirements I've so far defined, I'm going to go with choosing a board size first off.
There are plenty of board fabrication houses available, but my reading of various forums, blogs and other snippets
the web has to offer, seems to suggest that the Seeed Studio Fusion service is worth a try.

The service offers some preset "maximum" board sizes for fixed cost, some of which are useful here

  * 5cm x 5cm
  * 5cm x 10cm
  * 10cm x 10cm

I say useful here because I'm using the free version of [CadSoft Eagle](http://www.cadsoftusa.com/), which has a maximum
board size of 8cm x 10cm. Given the word layout is essentially a square array of letters, especially as I intend to use
a monospace typeface, I'll be looking at a square board. I don't see any benefit to adding space above, below or around
the words and it would reduce my options for producing a thin border in the housing.

So I'm left with square options with side lengths between 5cm and 8cm. The 5cm board is the smallest size they offer, at
about $10. Using the bigger 10cm board adds another $15 to the price. Since there's not a whole heap of components that need
to be added, and the boards being double sided, I think I can fit everything into the 5cm panel. It might be a little on the
rinky-dinky side, and almost certainly will need components mounted on both sides, but what's the point of this if there's
no challenge.

A 5cm x 5cm board it is.

## Components
Now I know how much space I have to play with, I ought to get round to defining what's going to fill it.
In the background I'm drawing up a schematic, which I'll include either in this post or a later one, but it's
pretty simple.

  * PIC16F1516 in either SOIC or SSOP
  * 32.768kHz crystal and two associated capacitors, all in SMD
    
    While it's a bit cheaper to use a T26 style PTH crystal, I'm going to try to avoid any PTH components
    and an SMD device allows me to get the crystal closer to the µC pins. Though I doubt that matters for this
    particular case

    RS 753-7265 (TXC 9HT10-32.768KDZF-T) R7.258ea [link](http://za.rs-online.com/web/p/crystal-units/7537265/)
  * a decoupling capacitor
  * five current control resistors
  * twenty LEDs
  * a 4mm x 4mm SMD tactile push button, for manual clock advance
  * ICSP header, likely a mini Molex thingy
    
    RS 670-0914 (Molex 87438-0542) R1.92ea [link](http://za.rs-online.com/web/p/headers-pcb-receptacles/6700914/)
  * battery mounts
    
    If I'm going to end up with N type cells, then
    RS 410-2560 (Keystone 55) R37.63/10 [link](http://za.rs-online.com/web/p/battery-holders-mounts/4102560/)

    If it's possible to use a coin cell type, then something else


![Schematic]({{ site.baseurl }}/images/2012-07-17-schematic.png)