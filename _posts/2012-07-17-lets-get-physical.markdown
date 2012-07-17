---
layout: post
title: Let's get physical
published: false
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

## Parts
 * ICSP header - RS 670-0914 (Molex 87438-0542) R1.92ea [link](http://za.rs-online.com/web/p/headers-pcb-receptacles/6700914/)
 * PIC16F1516/SSOP RS appear to have lost this!
   
   Not reported as EOL
   http://www.microchip.com/mymicrochip/Reports.aspx
   
   Available from https://www.microchipdirect.com/, for $10 shipping
   
 * 32.768kHz crystal - RS 753-7265 (TXC 9HT10-32.768KDZF-T) R7.258ea [link](http://za.rs-online.com/web/p/crystal-units/7537265/)
 * Battery mount - RS 410-2560 (Keystone 55) R37.63/10 [link](http://za.rs-online.com/web/p/battery-holders-mounts/4102560/)
 * 0805 LED via wellparts@eBay
 * 0603 passives via tedchen1632@eBay
 * 4mm X 4mm tactile switch