## TL;DR

Certain consumer DACs using Thesycon drivers can be suitable for professional use, as they likely support simultaneous ASIO and WDM output, making them a viable and cost-effective option for professional audio work for people not requiring any inputs on their audio interface.

## What makes a “pro” audio interface “pro”

Consumer devices mostly prioritize either the looks, the specs (such as supporting unnecessarily high sample rates or DSD), or sound quality (having some really good DACs, headphone preamps, low signal-to-noise ratio, etc.).

Professional audio interfaces usually focus on versatility (such as having way more channels than two), having input channels with or without microphone preamps, and, probably most importantly, stable drivers, since having ASIO working perfectly is crucial for professional use. Most of the time, though, professional audio interfaces don’t support ultra-high sample rates, DSD; they (at least in my opinion) don't look as nice, and they may even sound “worse” than the consumer ones. I put “worse” in quotes because it’s an open debate whether humans can actually hear the difference between “very good” and “way better than very good” DACs or preamps.

Another very important feature of professional audio interfaces is being able to simultaneously playback ASIO and non-ASIO (WDM) audio, which is kind of what this article is about. This feature is quite often supported in professional devices and is quite often lacking in consumer ones.

In consumer scenarios, ASIO is mostly used for listening to music. If a person cares about their digital signal path enough to use ASIO - it’s probably a good thing for them that they can’t hear any other sounds coming from their Windows mixer. On the other hand, professionals enjoy the ability to have their DAW running with ASIO and watch a quick video on YouTube or, most importantly for the game audio folks - hear the audio from the game they’re working on.

## Audio interfaces for game audio

Game audio workloads are slightly different from some other audio-related industries - there are quite a lot of people in game audio that don’t record any sound and don’t ever use any inputs.

If you need inputs on your audio interface - you could just stop reading this article and get yourself a professional audio interface with all the features you need. If you’re either working as a Technical Audio person or maybe even as an Audio Designer who doesn’t ever record anything using their PC - I have good news for you - there are way more audio interfaces that might suit your workflow than you probably ever thought.

## The good, the bad, and the ugly

There’s a whole lot of China-based manufacturers for consumer audiophile-grade DACs combined with headphone preamps. They usually come in three flavors:

1. Ones that don’t support ASIO at all;
2. Ones that support ASIO and use drivers made by ComTrue Inc. or Savitech Corp.;
3. Ones that support ASIO and use drivers made by Thesycon.

The first category isn’t suitable for professional use at all as it doesn’t support ASIO. The second one would be a pain to work with since ComTrue and Savitech ASIO drivers make ASIO exclusive - so when some software is pushing audio through ASIO, the WDM (regular Windows sound) will shut off completely.

The third category is the devices that are worth looking at.

**Thesycon drivers officially support mixing ASIO and WDM** as long as they’re running at the same sample rate (which is fine; most professional audio interfaces work the same way).

## How to choose an audio interface

So, let’s say you’re looking at some consumer DAC with a headphone preamp to use as a professional audio interface. I assume you’ve already evaluated some basic features such as that it has all the outputs you need, looks nice, etc.

1. The first thing you’ll need to do is to make sure it uses Thesycon drivers. You could do this by just:
    1. visiting the manufacturer's website,
    2. downloading and installing the drivers for the particular device you’re interested in,
    3. opening the folder with the installed drivers, right-clicking on any of the .dll or .exe files there, opening Properties,
    4. and looking either for “Thesycon” in Digital Signatures or for “TUSBAudio” in the Details pane.
    
    The easier way is just opening the control panel for the device and making sure the window looks exactly like this (with the only difference being the manufacturer name in the window title):
    
2. Next - try to find some reviews and measurements! I won’t be going deep into this - you’ll need to do your own research on understanding the numbers and everything, but looking for reviews on either https://www.audiosciencereview.com/ or https://www.l7audiolab.com/ might be helpful in understanding whether it’s an actually good audio interface.
3. Make sure the drivers are up to date. The latest version of Thesycon drivers at the moment of writing this article is around 5.60-something. It’s easy to find the current version of Thesycon drivers using Google. If the version on the manufacturer’s website is very old compared to the one you found - it means that there might be some compatibility issues on newer Windows versions.
4. Contact the manufacturer and make absolutely sure that it supports the simultaneous output of ASIO and WDM.
5. That’s it!

## My own experience

This whole research into drivers actually came from my own experience when I had to give up my corporate-owned Apogee Groove that I used for the last few years and buy myself my own audio interface. While I did like the Groove - it’s quite expensive and it has its own quirks with volume adjustment, so I was looking for some ways to both get an interface that's at least as good as Groove and save some money. The interesting thing about the Apogee Groove, though, is that it uses the exact same drivers I’m talking about in this article - Thesycon.

I ended up with the Topping DX1, which both looks great, has a very nice-feeling volume adjustment knob, spec-wise is even better than Apogee Groove, has additional outputs for speakers (that use the same two channels as the headphone amp), and with all mentioned above - costs 2 to 2.5 times less than Apogee Groove. The drivers and ASIO are also working perfectly, exactly the same as it was with Apogee (which is kind of expected given that they use exactly the same drivers).

## Some device suggestions

I tried to find some DACs with headphone preamps that are not too expensive (<$200) and use Thesycon drivers.

Here’s what I found:

- Topping (most DACs);
- SMSL (most DACs);
- FiiO KA1, KA13, KA17, K3, New K3, K5Pro, K5 Pro ESS, K7, K11, E10K-TC, and some others;
- JDS Labs Atom, Element series;
- Khadas Tone series.

I cannot confirm that each and every one of them is a good DAC and that ASIO+WDM works perfectly for any of these devices apart from the Topping DX1 I have. However, if you choose something from this list and follow the steps I described in the “How to choose an audio interface” section - there’s a good chance you’ll end up with something nice in the end.
