---
layout: post
title: A PICing puzzle
---

## PICking the _right_ chip
One of the great things about the MicroChip line of PIC controllers is that they make _so_ many different versions.
One of the bad things about the MicroChip line of PIC controllers is that they make _so_ many different versions.

That might sound a bit crazy, but I'm going to be looking for a set of features and it's quite likely that there will
be a number of distinct versions which will fulfill the requirements.  There may well be a chunk of time dedicated to
sifting through the options to find one that's _just right_, rather than _suitable_. There will be, I know because
I've sort of started looking, cases where the controller has the required features, but packaging issues make its use
somewhat more complicated than it might be.

So, before I go off to the datasheets, what am I looking for

### Requirements

#### Battery Powered
Duh! But it's worth listing up front, even if only to remind myself to pay attention to power usage. Though I severely doubt
the µC is going to consume anything like the power of the LEDs.

#### 32.678kHz watch crystal driver
This thing is meant to keep time, hopefully more accurately than peeking out the window on a sunny day. Watch crystals are cheap
and accurate (~20ppm). A PIC internal oscillator is typically calibrated at the factory to 1%. Lets just work out what that means
in the use case here:

	24 hours = 1440 minutes
	1440 * 0.01 = 14.4 minutes

That's nearly a quarter of an hour error, __per day__!

A watch crystal, at 20 parts per million, manages in the order of 2 __seconds__ per day error, or something like a minute per month.
Not sure about you, but I prefer that one, right there!

So this clock thingy needs to have something like a watch crystal driving it. It's accurate and doesn't cost more than a few cents.

Why 32.768kHz? Well, they don't make them in these odd numbers because they think it's lucky. 32768 is exactly what can be stored in a 15
bit value. If you happen to have a 15 bit counter driven by the crystal, you know that when the counter overflows a second has passed.
Now, a 15 bit counter is pretty unusual, but because of the way binary numbers work, you can easily make use of a 16 bit counter, and these
things are a tad more common.

I'm not going to explain how binary counting works, Google has plenty of better answers to that than I could conjure, but suffice to say
that setting the most significant bit high when you reset the counter will provide an overflow on 32768.

#### 16 bit counter
Which leads me nicely onto the next requirement, a 16 bit counter. If I'm going to be using the crystal to watch the seconds tick by it's
going to be a lot easier with a built in 16 bit counter. It would be entirely possible to do so with an 8 bit counter and an 8 bit register
but that seems like a bit too much work.

Bonus points for being able to take input from the crystal directly and operate while the µC is asleep. I'm guessing here, but if the µC
can sleep while time is passing, and be woken when it needs to do something, it might save a bit of juice. This might be especially useful
if the software knows about nighttime and chooses to switch off the LEDs when everyone is looking at their eyelids.

#### Enough I/O
OK, so I bailed on the decision [earlier]({{ site.baseurl}}/2012/07/03/figuring-the-ins-and-outs.html) about just how I'm going to drive
the LEDs, so it's a bit difficult to actually say what is _enough_. But I can put some bounds on the issue.

 * Shift Register = 3 I/O
 * Multiplex = 5x4 = 9 I/O
 * Charlieplex = 5 I/O

So I'm going to need, bare minimum, 3 pins available, and at most 9. Also worth noting is that these would all need to be input _and_ output
pins. Some pins seem to be limited to input only, maybe because they share the ^MCLR function. In any case, these all need to be able
to output stuff.

Besides driving the LEDs I need some way to set the current time. It's all well and good having something that can count nicely and whatever,
but sitting around till midnight to replace the battery seems like a pretty odious requirement. A simple input, driven by a push button of
some sort, should be enough to advance the clock manually.

### Sifting the chaff
So I know basically what I need from the poor victim of my experiment, I guess I ought to shuffle the deck and see what MicroChip has
to offer.

http://www.microchip.com/productselector/MCUProductSelector.html

A quick check says PIC10 has nothing on offer, no 16 bit counters and 8 pin packages, I'm pretty sure there's nothing useful there.
PIC12 has plenty of devices offering 16 bit counters, but only one that I can see might be interesting, PIC12LF1840T48A. Sheesh, that's
a mouthful.

#### PIC12LF1840T48A
 * 1 16 bit counter with dedicate 32kHz driver
 * 5 I/O and 1 input only pin
 * Pins don't look to have significant complications, like ICSP conflicting with the XTAL
 * XLP
 * TSSOP package
 * Most expensive PIC12 on offer

I would _have_ to use shift registers to use this thing, and a cursory glance at my local providers suggest they know not of its existence.
OK, I could use Charlieplexing, and the remaining pin for the clock advance. It's a close shave, but it might work, so I'm not entirely
discounting it.

On to the PIC16 range, of which there are __many__

It seems like the crystal driver is not something deemed important enough to provide a filter on, so this is getting tedious.

#### PIC16F151[6789]
 * Available in 28 pin package
 * 32kHz driver
 * 16 bit counter
 * ISCP doesn't conflict with XTAL
 * Seems to have plenty of I/O ports
 * Available locally (RS ZA ~R20ea)

A potential winner, and strangely something I hadn't spotted before.

Looking at the pin allocation table from the datasheet, ICSP and MCLR are on pins that can be dedicated, which will make life a bit easier.
SOSCI/SOSCO, which seem to be the pins for the Timer1 crystal driver, don't seem to conflict with anything I need.
MCLR, on the 28 pins packages, don't conflict with anything, which means the I/O is straightforward. No weirdness with an odd pin in the
middle of RA where a pin is input only. Actually looking quite tasty.

So I'm going to adopt this little bugger and move on. It's entirely possible I'll have to come back and choose another,
but for the moment I'm pretty certain that _somewhere_ in the PIC16 range is something useful, and I'm going to use this one to start with.

### So what was I wittering on about earlier?
I mentioned that there's cases where packaging or whatever get in the way, and I was expecting a few cases of this while looking tonight
for the chip of my dreams.

I have a few PIC16F1827's, which I think I ended up with because PIC16F1936 wasn't available, and that was the version suggested by
someone in the know. In any case, the 1827 shares the T1OSCI/T1OSCO pins with ICSPCLK/ICSPDAT, which, frankly, is a pain in the proverbial
butt hole. Without figuring out if my particular crystal can handle the signals from the programmer I would have been left with some
half-assed solution to isolate the programmer from the crystal once the board was together. I'd much rather spend a few bucks and get
some other version where there's no conflict.
