---
layout: post
title: Laying out the words
---

One day my news feeds highlighted an article about
[Building a word clock with genetic algorithms](http://hackaday.com/2012/04/10/building-a-word-clock-with-genetic-algorithms/).

Armed with a bit of Perl and a desire to improve on the, at the time, minimum size English clock of 11x11, I fired up TextMate.

I'm not going to post up the code, it's basically a bit embarrassing, but it did lead me to a useful arrangement.
We're a bit lucky in the English language given how times can be constructed, and this lead naturally to a fairly efficient set of phrases for the 5 minute segments

  - [hour] o clock
  - [five|ten|quarter|twenty|twenty five|half] past [hour]
  - [twenty five|twenty|quarter|ten|five] to [hour]

In effect I just needed to arrange a sequence of 6 word groups:

  - ten, twenty
  - five
  - quarter, half
  - past, to
  - one ... twelve
  - o clock

The ordering of the words _within_ the groups was not important to the construction of the phrases, just the ordering _of_ the groups.
However, getting the words arranged into the smallest possible grid did mean the ordering of words within the groups had an effect.
In the end I manually arranged the words within the groups to fill the smallest grid I could.

    twenty ten
    five  half
    quarter to
    past three
    fourtenone
    eight five
    elevennine
    two  seven
    six twelve
    o clock

You will note that there are situations where words are abutting each other.
This is allowable in those situations, since those words will not be used together in any phrase.
A example is the fifth line, where [four], [ten] and [one] are all squeezed together.
But these words are only even used to denote the hour, and I'm not aware of any clock system where that might be an issue.
Certainly notthe one I choose to understand day by day.

So there it is. I'll be building a 10x10 matrix of letters, some of which happen to form useful words in sequences that allow me to spell out a reasonable approximation of the current time.