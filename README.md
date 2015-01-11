# Infrared Bird Box

A bird box with a Raspberry Pi infrared camera inside.

[![](images/cover.jpg)](http://www.gardman.co.uk/wild-bird-care)

This project will not only teach you about electronics and programming, but can help support the bird population in your area. Having a camera inside a nesting box can be tremendously rewarding; however, with the Raspberry Pi you can also share the nesting box with the world by streaming the video content to the Internet. Watch as your birds gain their own Internet following!

## Lesson objectives

- Appreciate the nesting needs of wild birds
- Understand visible and infrared light
- Understand the principles of focal length and depth in photography
- Understand video streaming and content distribution services

## Lesson outcomes

- To have made a bird box with a night vision camera inside
- To have live streamed video content from the bird box to the Internet

## Requirements

As well as a Raspberry Pi with an SD card loaded with Raspbian, you'll also need:

### Hardware

- Raspberry Pi NoIR Camera Board - has a **black** circuit board (try [CPC](http://cpc.farnell.com/jsp/search/productdetail.jsp?sku=SC13223))
- **Female** to **Female** jumper wires, at least 3 (try [Pimoroni](http://shop.pimoroni.com/collections/components))
- 220 Ohm 1% Resistor; get several in case of breakages (try [Pimoroni](http://shop.pimoroni.com/collections/components))
- Infrared LED 5mm 890nm; get several in case of breakages (try [RS](http://uk.rs-online.com/web/p/ir-leds/6997663/))

### Software

- FFmpeg (internet streaming software, instructions are provided on the worksheet below)
- Any web browser to access www.ustream.tv

If this resource is going to be used in a class environment, it will save a lot of time if the *Compile FFmpeg* section under step 5 of the worksheet is done prior to starting the lesson.

### Extras

- Bird box (try [B&Q](http://www.diy.com/nav/garden/pet-bird-care/bird-care/nesting_boxes/Gardman-Wild-Bird-Nest-Box-9374965))

### Time required

- 2-3 hours

## Worksheet & included files

- [The worksheet](worksheet.md)
- [Advanced second worksheet](worksheet2.md)
- (Optional) Final version of ustream script [ustream](https://raw.githubusercontent.com/raspberrypilearning/infrared-bird-box/master/code/ustream)
  - Download to your Pi with `wget https://raw.githubusercontent.com/raspberrypilearning/infrared-bird-box/master/code/ustream --no-check-certificate`

## Disclaimer

This resource will walk you through overcoming the technical hurdles to have a working live webcam inside your bird box. However, it does not cover the DIY challenges required to protect your equipment from the elements. Overcoming those is your own responsibility, and will be quite a fun and motivating activity in its own right.

## Licence

Unless otherwise specified, everything in this repository is covered by the following licence:

![Creative Commons License](http://i.creativecommons.org/l/by-sa/4.0/88x31.png)

***Infrared Bird Box*** by the [Raspberry Pi Foundation](http://raspberrypi.org) is licenced under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

Based on a work at https://github.com/raspberrypilearning/infrared-bird-box
