---
author: David der Nederlanden
category:
  - coffee
date: "2026-06-24T12:05:01+00:00"
tag:
  - reverse-engineering
  - ai
  - diy
  - coffee
  - agentic
  - espresso
  - microcontroller
title: My attempt at fixing a bug in the Eureka Mignon Specialita Display
url: /eureka-mignon-specialita-display/

---

Last December, I decided to get into espresso making. I used to buy pre-ground coffee from [Illy](https://www.illy.com), which I was quite okay with.
However, after really diving into my [Quick Mill 820's](https://www.quickmill.nl/product/quickmill-820/) inner workings, I decided it was time for a real coffee mill.
I bought my Quick second-hand, as all of its components are replaceable, which I was okay with if needed.

After researching different types of coffee mills for some time, and the webshops selling them, I decided it wasn't worth it at that moment.

## One week later

That moment of not being worth it, lasted a week.
One morning, I stumbled upon [someone's project where he made a grind-by-weight mod](https://github.com/jaapp/smart-grind-by-weight/tree/main) for the [Eureka Mignon Specialita](https://www.eureka.co.it/en/products/eureka+1920/mignon+grinders/silent+range/20/).
As a maker, I decided this was the signal I needed.
I ordered the Eureka new, along with all the parts from AliExpress for the mod, and was ready to immediately mod it upon arrival.

I chose a new Eureka, because the motor of it is the most important part, and it isn't a cheap spare part, it's basically the whole grinder, so I wasn't willing to take a risk there.

The Eureka arrived and I was actually quite happy with the out-of-the-box experience, because it was simple, hassle-free and offline!
Even with grind-by-weight, there are still other grinding factors, like how full the hopper is, because that weight pushes the coffee through the grinder. 

So since I still didn't have a scale that was able to weigh with 0.1g precision,
I decided to use all the parts for the GBW mod to basically build a scale at that point, and designed a [housing](https://github.com/jaapp/smart-grind-by-weight/issues/83#issuecomment-3708450346) around it.
When dialing in beans, I briefly use the scale and then it goes back into my cabinet, the consistency of the timer is just enough for now.

## The Infamous Timer Bug

Fast forward to now. One morning, my double-shot grind timer suddenly went off at 9.6s. When I tried to bump it to 11.9s, which was my setting the day before, the '+' button didn't respond. 

[A quick web search revealed](https://kaffeemacher.de/en/blogs/kaffeewissen/eureka-mignon-display-problem) that this was a known bug for a long time.
Thus, I immediately wrote to my supplier and they dealt with it very promptly.
They sent me a new display under warranty so I could replace it myself, as they've seen it more often in the past.

Me being someone who thinks a lot, it still annoyed me, as the reason why was unclear.
Knowing that it could happen again anytime even with the new display, I kept searching.

## Reverse Engineering the Firmware

The already very revealing blog above sent me to this [write-up](https://denshaotoko.github.io/blog/2024/10/31/eureka-touchscreen-repair.html) of Johannes,
who dug into the microcontroller driving this mill.

His write-up quickly caught my attention and I ordered the programmer so I could dump the firmware myself too,
as I thought that now with AI, it must be pretty doable to at least do an investigation of the code, even if it was in Intel HEX format.

The board uses a Microchip PIC16F1936, which has options for read / write protection, but luckily it isn't set by the factory.

The [PICKIT 3](https://www.microchip.com/en-us/development-tool/pg164130) (a clone) arrived and I quickly dumped the firmware.
I threw it into [Gemini's](https://gemini.google.com) and [Claude's](https://claude.ai) web UI, which already revealed promising results, but being on the free tier, I was limited.

After reading a bit on some models, I decided to use the [Deepseek API](https://deepseek.com/) in combination with [Claude Code](https://claude.com/product/claude-code) and started chatting away.
At work we use Claude with Claude Code, but I don't really like the subscription model, I don't do this daily and having read good things about the usage based API of Deepseek made me choose them for this.

I clearly explained CC the bug, my assumptions, and what I'd like to get out of it, and it went on it's journey in the Assembly code.

I used AI for this because I figured I might be not as good or quick as a machine that's already very well trained on this type of code and explaining it to me,
and surprise surprise, it did a really great job, but more on that later.

### Testing the Assumptions

My assumption was that if you adjust the timers and then turn the mill off too quickly, the timer gets corrupted in the EEPROM as the writes are interrupted.

Although I am always cautious with AIs checking my assumptions, as they'll easily admit I'm right,
it did find that the time values are stored at two addresses in a [little-endian](https://nl.wikipedia.org/wiki/Endianness) fashion.

This is interesting, because if power is cut mid-write, you'd likely end up with a huge number. 

What was also found is that upon boot, this number isn't verified.
There is a valid range in which you can adjust the timer yourself, but a non-valid value is just read and put into memory upon boot.
This aligns with Johannes' write-up where a toolless fix was mentioned: pressing the '-' button for roughly 23 minutes to fully countdown the number, which indeed worked!

## Trying to make a Patch

I asked Claude Code to implement a validator. If the value that is read into memory is outside the allowed range, it sets the timer to 0.3s.
I chose this number because the minimum is 0.2s and it is really short;
if you don't notice it, you won't end up with a counter full of coffee grounds, and the 0.3s still allows you to differentiate clearly from the factory minimum.

## Testing the Patch

At this point, having two displays available, I decided to flash one of them and just run it.
To my surprise, it really worked! I tested all kinds of scenarios by setting different values in the EEPROM deliberately, and it did indeed correct them just fine.
The other functions remain too, or at least, I didn't find any regressions.

## Fixing Your Own Eureka

To make this complete, without just dumping the patched firmware on the internet, Claude and I made a small open-source tool which allows you to patch your own dump of the firmware.
It even validates if your dump is the same as mine. Most likely it will be, as this bug has been there for a while. 

If you can't or don't want to flash it yourself, you can also contact me and we'll figure out what's possible.

My take at fixing this bug in full technical detail can be found [here](https://github.com/randommen96/eureka-pic16f1936-patch). Beware, it is made with AI and as we say in Dutch, *"garantie tot de voordeur"*, or maybe *"it runs on my machine"* is more applicable here...

## What next

Although this patch works, I've always enjoyed challenges where electronics, software and hardware come together,
so together with Claude Code I'm fully disassembling the code and trying to make the firmware even better, possibly even letting the AI fully rewrite the codebase.

![Flashing the Eureka Mignon Display](/images/eureka-timer-patching.jpg)
