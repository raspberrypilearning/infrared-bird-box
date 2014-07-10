# Infrared Bird Box

A bird box with a Raspberry Pi infrared camera inside.

[![](images/cover.jpg)](http://www.gardman.co.uk/wild-bird-care)

This project will not only teach you about electronics and programming, but can help support the bird population in your area. Having a camera inside a nesting box can be tremendously rewarding; however, with the Raspberry Pi you can also share the nesting box with the world by streaming the video content to the Internet. Watch as your birds gain their own Internet following!

This resource will walk you through overcoming the technical hurdles to have a working live webcam inside your bird box. However, it does not cover the DIY challenges required to protect your equipment from the elements. Overcoming those is your own responsibility, and will be quite a fun and motivating activity in its own right.

##Lesson objectives

- Appreciate the nesting needs of wild birds
- Understand visible and infrared light
- Understand the principles of focal length and depth in photography
- Understand video streaming and content distribution services

##Lesson outcomes

- To have made a bird box with a night vision camera inside
- To have live streamed video content from the bird box to the Internet

##Time required

- 2-3 hours

##Requirements

- Raspberry Pi
- Micro USB power adaptor
- An SD Card with Raspbian already set up through NOOBS
- USB keyboard
- USB mouse
- HDMI cable
- Ethernet cable
- LAN with Internet connection
- A monitor or TV
- Raspberry Pi NoIR Camera Board - has a **black*- circuit board (try [CPC](http://cpc.farnell.com/jsp/search/productdetail.jsp?sku=SC13223))
- **Female*- to **Female*- jumper wires, at least 3 (try [Pimoroni](http://shop.pimoroni.com/collections/components))
- 220 Ohm 1% Resistor; get several in case of breakages (try [Pimoroni](http://shop.pimoroni.com/collections/components))
- Infrared LED 5mm 890nm; get several in case of breakages (try [RS](http://uk.rs-online.com/web/p/ir-leds/6997663/))
- Bird box (try [B&Q](http://www.diy.com/nav/garden/pet-bird-care/bird-care/nesting_boxes/Gardman-Wild-Bird-Nest-Box-9374965))

###FYI for teachers

If this resource is going to be used in a class environment, it will save a lot of time if the [Compile FFmpeg](#compile-ffmpeg) section of step 5 is done prior to starting the lesson. I would also recommend duplicating the SD card as many times as is necessary after compiling is complete.

##Introduction

To begin with, pupils should appreciate that garden birds are very choosy about where they build their nest. The bird box will need to be located out of any predator's reach, away from any prevailing winds and nowhere near a bird table or feeder.

Once a bird has moved in, the box must not be disturbed until they have finished breeding; this is usually between October and January in the UK. If something goes wrong you can't just open the box and fiddle with your wires or adjust the camera, as this will traumatise the birds and could cause eggs or hatchlings to be abandoned.

A requirement of the system is to see the birds in total darkness. A light inside the bird box could attract insects and predators, and therefore no birds would select it as a nesting site. It is possible, however, to illuminate the inside of the bird box with a kind of light that is invisible to animals and humans, but *is- visible to a camera. This is commonly known as night vision. Night vision works by using a spectrum of light called [Infrared](http://en.wikipedia.org/wiki/Infrared) which has a longer wavelength than visible light. Notice that IR is to the right hand side of the visible spectrum of light below:

![](images/spectrum.jpg)

Look at the night vision surveillance camera below, for example. Around the camera lens, there are lots of infrared LEDs (light emitting diodes). These emit infrared light which will then bounce off various objects and return to the camera lens, allowing it to create an image.

![](images/surveillance.jpg)

The image will look black and white (greyscale) because there are no wavelengths of light from the visible spectrum being detected. However, a black and white image is good enough to allow you to watch what is happening inside a bird box, and it doesn't disturb or interfere with the birds in any way.

![](images/pinoirada.jpg)

Pictured above is the special version of the Raspberry Pi camera board called Pi NoIR. It's essentially identical to the normal green camera but it has no infrared filter, meaning that it lets in infrared light. This camera, combined with an infrared light source, will give you night vision. It's also small and won't be too intrusive when mounted on the inside of a bird box.

## Licence

Unless otherwise specified, everything in this repository is covered by the following licence:

![Creative Commons License](http://i.creativecommons.org/l/by-sa/4.0/88x31.png)

***Infrared Bird Box*** by the [Raspberry Pi Foundation](http://raspberrypi.org) is licenced under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

Based on a work at https://github.com/raspberrypilearning/infrared-bird-box
