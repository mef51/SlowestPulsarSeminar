Oct. 11

1. My background
2. Background of the object
3. Light-curve from the paper
4. How the observations were made (Swift, BAT)
5. The rest of the observations
6. Background on Supernova Remnants and Classifying 1E 1613
7. Spin down scenario
8. Conclusion and Graph of pulsar periods

***1.***

Hi everyone, good afternoon.
As some of you know I did my undergrad at the university of Ottawa. My undergrad research wasn't astronomy related; I spent one summer doing computational neuroscience where I built a simulation model in the hopes of studying the nerve damage that can happen in patients with diabetes, and I spent the last year of my undergrad working at the 3MV tandetron, which is used to do extremely sensitive mass spectrometry and mostly radiocarbon dating. Both were interesting projects But I wanted to do an astronomy talk so in the lack of any astronomy related research experience I went to NASA's Facebook page and scrolled through their posts until I found this.

***2.***

This is the supernova remnant RCW 103. Its age is about 2000 years and it is 3kpc away in our galaxy. It was discovered about 25 years ago and at its center is a compact xray source called 1E 1613 (which I'll just call 1E for now). Long observations made of 1E found that its xray flux varies with a period of 6.67 hours, which is much longer than the periods observed for other compact objects left behind by supernovae. Pulsars normally are observed to have periods of milliseconds to at most minutes, and while the relatively new idea of magnetars was a possible way to explain the extremely slow period there wasn't enough 'confirmed' magnetars for this to be a convincing classification. We'll go into more detail on pulsars and magnetars later; the other possible explanation for this 6.7 hour period is that the object is really a binary system with a companion that occludes the xray source. But a 6.7 hour period means that the binary system is very tightly bound, and on in addition is not very bright, since optical observations don't show a source. If 1E really is a binary system, the companion is a low-mass late type star that had to survive a supernova 2000 years ago. So in light of all this what new evidence would shed more light on how to classify 1E? And what could we observe that will allow us to distinguish between a binary system and an isolated system, and then tell us parameters about that system?

***3.***

It sounds like a difficult problem but it might not actually need that much to solve it. In fact it looks like just ten milliseconds might be enough. On June 22nd this past summer the Swift telescope detected a 10ms long burst in xrays coming from RCW103, which is what this paper I'm presenting analyzes. Here you can see the lightcurve of the burst from Swift.

Notice we have the Count-rate vs. the time in ms, and notice the energy range of 15-350 keV, which is around the hard xrays and gamma rays part of the spectrum. The timing resolution here is 2ms; each of these points corresponds to 2ms of data. You can see that there two peaks in the burst and that the burst ends suddenly, and there isn't really a tail.

The more I stared at this the more it bothered me that the peak count rate is 6 counts per second. Over a timespan of 2ms, this is much less than a single count (Its actually about 0.01 of a count).I didn't mind this at first and I thought it was just a typo on the axis but here is another light curve in another paper by a different group about the same burst. They distribute the energy range differently but you can see the counts are of the same order of magnitude. They still seem too small. It's unlikely they both made similar typos and that none of the 10+ authors noticed the mistake. So what is going on in this lightcurve, do the actual count rates make sense, and is this burst actually something substantial?

***4.***

To make sense of this we can look at ways that xray astronomy is done and then look at the Swift telescope specifically.

The first fact you need to deal with if you want to collect xray photons is that the atmosphere is opaque to them. Okay, no problem, that's why Swift is a space telescope.

The second fact you need to deal with is that xray photons will pass straight through lenses at normal incidence. As far as I could tell there isn't any material that you can make your lens or mirror out of that will focus an xray image the way an optical image is focused.

This fact is harder to deal with, and there are two main ways to deal with it.
The first way is to do grazing incidence optics. Though xrays will pass straight through a lens at normal incidence, it is actually possible to build a mirror that will reflect xrays that come in almost parallel to the mirror, for incidence angles usually less than 2degrees. It's then possible to build telescopes out of just grazing xray mirrors, and that's called a Wolter telescope after the guy who came up with it. Here's an image of NuSTAR which is a Wolter type telescope. Chandra is also a Wolter type telescope and so is one of the instruments on board Swift, but not the instrument that detected the burst. Wolter telescopes can give you high resolution but their field of view is very narrow, and Swift finds bursts by looking at a large piece of the sky at once.

It does this by not using mirrors or lenses at all. Though the only mirrors that will affect xrays are the grazing type mirrors you can build CCDs that will detect xrays without a problem. So you can imagine that if you want to cover a large portion of the sky you can just make a large array of detectors and you'll know when a burst happens fairly easily. To know where the source came from you can use a coded aperture mask, which is the second big way to do xray astronomy. The coded aperture is usually some random pattern that is placed above the detector at some fixed distance so that the light has to pass through it before it hits the detector. Then any light that passes through the aperture will leave a pattern on the detectors. From this pattern, and knowing the distance to the aperture you can do raytracing and other computations to figure out where in the sky the source was. The tradeoff with this technique is the resolution; while you can cover a wide area of the sky you will never get images like Chandra does.

So with that in mind here's a graphic of the Swift telescope, which is really three instruments sharing the same spaceship. Swift has an Xray telescope (XRT) which is the greenish tube in this image, a UV/Optical telescope (UV/OT) which is this reddish tube and the Burst Alert Trigger or the BAT which is this massive D-shaped object. Notice the coded aperture mask and the array of detectors below it.

For scale this is an image of the aperture. It's several meters long, and the pattern is uniformly random with half the tiles open and half the tiles closed. The closed tiles are made of lead and I imagine that they're set onto a rigid material that is transparent to xrays so that's its actually possible to mount this above the detectors. You can kinda see that there are tiles not connected to anything and would just fall through otherwise.
Here is an image of one of the detector modules that make up the detector plane. On BAT there are 32768 detectors, which is 2^15, and any of these detectors can fail and will change the way you do the analysis. I find it mind-blowing that this procedure of raytracing through a coded aperture works at all in practice. It still feels like magic to me. If you find it interesting there's a field called computational photography that this falls under, and it's also relevant in things like computer vision.

So back to our original problem of understanding this light curve from BAT, we now know that these photons were collected through a mask aperture and that they fell on an array of at most 32768 working detectors. I asked around online and was pointed to the specs for a program from NASA used to compute light curves from the BAT counts. Reading the usage info, there's a parameter called "detdiv" that defaults to YES. Set to YES if you want the rate to be per detector. If no detector mask is supplied then the rate will be divided by the total number of detectors (32768). The detector mask is just for the program to know which detectors were actually on.
But this solves our problem, going back to this lightcurve we now look at these rates as per detector, and at the peak count rate of 6 per second per detector its really about 200,000 counts per second, which over this timespan is about 400 counts.

Now that we know how the data is collected lets look at the rest of it.

***5.***

After BAT detects a burst and calculates the source it decides if its worth pointing the XRT and UV/OT at the object to take higher resolution observations. Luckily BAT decided it was worth checking out (making BAT an example of an early robot overlord), and so we have this soft-xray image of the object after the outburst. On the right is all the observations before the burst stacked into on image and on the left are all the observations starting after the burst, starting about 100s after the burst. The blue is at most 10keV and is the highest energy. Notice that it's much brighter than all the observations from before, and the dashed circle is the error circle for the position calculated by BAT.

The residual brightness can also be seen in this long term lightcurve by XRT. The dashed line represents the burst. You can see that it drops quickly but doesn't return to the pre-burst level.

The UV/OT telesccope also took long exposure observations in various filters and here they are. The circle is the Chandra position of the object. Red is brightest. There's seems to be a source in the V band that overlaps with the error circle, and based on its magnitude the authors say that if this is a companion it is at most a late-type low-mass star.

After the trigger was announced to the world the GROND observatory in Chile started taking observations as quickly as they could and here we have their data from green bands on the left to infrared bands on the right. The little circle is again the Chandra position. Black is brighter.Notice the large source in the r' band which we saw from Swift UV/OT, but no source at the Chandra position.

***6.***

So these are the observations we have to deal with, now to make sense of it what do we know about supernovae and their remnants? What do we expect to get left behind that might be 1E 1613?

So BOOM you have your supernovae, hot gas goes spewing forth in all directions, and what gets left behind in the center? Well you can have a black hole if the star's mass is high enough, you can have a neutron star when the star's mass is a little lower, and you can have a white dwarf if the star's mass is about the mass of our sun. Neutron stars are made up of matter that is so tightly squeezed the neutron degeneracy pressure keeps its shape and white dwarfs are made of matter held up by electron degeneracy pressure.

Since we have this pesky variability to deal with we need to also assume that there's a way for a binary system to be left behind.

Let's rule some out now.
It's not a black hole. There are a lot of background stars and we see no lensing.
It's probably not a white dwarf. It's too bright, which points to a higher mass than expected for a white dwarf. Fess up if people ask about this.
Neutron Star. All pulsars are neutron stars, so pulsars fall under this category too. We almost want to rule this out as well because we've never seen pulsars  with such low spin periods.

Let's look more closely at pulsars.
A pulsar is a highly magnetized neutron star. It emits beams of radiation from its magnetic north and south poles which we can see when they point towards earth. This radiation seems to pulse since the magnetic axis is not lined up with the rotational axis and so this period of pulsation is the spin period of the neutron star. They were first discovered in 1967, just a few years before RCW103. Pulsars don't always emit in xrays, but many have been observed to, so this wouldn't be the first. Of the xray pulsars we've seen the slowest has had a spin period of 681s, or about 11 minutes. Many pulsars have spin periods of just seconds and some have periods in the millisecond range. This would certainly make our object an outlier.

Now under pulsars we have a further subdivision of magnetars. Magnetars are a new idea, and their theory was developed in 1992 by Robert Duncan and Chris Thompson. In this theoretical paper they explain how during the formation of a neutron star, certain conditions could lead to it being very strongly magnetized. These magnetars according to the theory would have field strengths of 10^14-10^15 G, compared to 10^12 G for regular pulsars.

Now, according to the theory these intense magnetic fields would power strong high energy bursts as they decay. On top of that, the theory predicts that the rotation of such a strong a magnetic field means that after a burst the intensity will recover to a higher level than before. Sound familiar?

Because our object had a burst at all in hard xrays and gamma rays, this points immediately to a strong magnetic field. Returning to a higher intensity also seems to be what's happening based on this figure.

But finally, the reason our object is probably not a binary system, is because measurements of the 6.67 hour period made after the burst are phase shifted relative to before the burst. That is the observations of the variability don't line up with the sine wave extended in time after the burst.
This would imply that the poor companion star stopped in its tracks momentarily or had its orbit interrupted by the xray burst. There just isn't enough energy in 10ms xray burst to do that.

So Magnetar it probably is. The 6.67 hour variability is now the spin period of the magnetar.
Even amongst other likely magnetars, this spin is much much slower. If for a moment now we totally accept that this is a magnetar and remembering that the supernova is 2000 years old, what physics can explain this dramatic spin down?

***7.***

The paper goes into several different possibilities for how a neutron star could slow down this quickly but I'll just show their favorite explanation. They first make the case for why the newly formed magnetar would have a fallback disk with significant mass. This is material that starts to fall back onto the star after the supernova. This argument is complicated and I don't understand it, so let's just accept that it's there. Now the material in this disk will be hot and some of it will be plasma. The strong magnetic field of the magnetar makes the interaction with this material particularly strong. So as this material passes through the magnetic field and falls back onto the magnetar, the spin period slows down.

I didn't immediately understand how this happens so here's an analogy. Replace the star with a carousel. The carousel is spinning under its own inertia, and it has some angular momentum. Now imagine the disk of material is really a pack of rabid sugar-high children, running full throttle towards the carousel. They all jump onto the carousel. As they jump onto the carousel, it will slow down. Therefore magnetars with fallback disks will slow down quickly.

The details in the paper are much more complete and even rely on some simulations so if you're interested please look there.

***8.***

So to summarize, we looked at the recent burst from the central object in the supernova remnant RCW103 and talked about how it was hard to classify because of its strange 6.67hr variability in soft xrays. After much meandering we concluded it was probably not a binary system because the phase of the variability changed. I explained why it was probably a magnetar because the burst of hard xrays fits what is expected from magnetar theory and also its late spectrum settled at a higher intensity than before the burst also expected from the magnetar theory.
Then we explained that the magnetar probably slowed so much because of the interaction of its magnetic field with a fallback disk. Thusly a mystery from 1974 was resolved and 1E 1613 is therefore

PROBABLY THE SLOWEST PULSAR EVER

Thanks for listening.
Sources.
