Infrared Bird Box
=================

A bird box with a Raspberry Pi infrared camera inside

[![image](./images/cover.jpg)](http://www.gardman.co.uk/wild-bird-care "Wild Bird Care | Gardman")

This project will not only teach you about electronics and programming but can help support the bird population in your area.  Having a camera inside a nesting box can be tremendously rewarding, however with the Raspberry Pi you can share the nesting box with the world by video streaming the content to the Internet.  Watch as your birds gain their own Internet following!

This resource will walk you through the technical hurdles to allow you to have a working live webcam inside your bird box.  However it does not cover the DIY challenges required to protect your equipment from the elements.  Overcoming those is your own responsibility and will be quite a fun and motivating activity in its own right.

##Lesson objective
* place holder

##Lesson outcome
*	place holder

##Time
*	2-3 hours

##Requirements
*	Raspberry Pi
*	Micro USB power adapter
*	An SD Card with Raspbian already set up through NOOBS
*	USB Keyboard
*	USB Mouse
*	HDMI cable
*	Ethernet cable
*	LAN with Internet connection
*	A Monitor or TV
*	Raspberry Pi NoIR Camera Board - has a **black** circuit board (try [CPC](http://cpc.farnell.com/jsp/search/productdetail.jsp?sku=SC13223 "RPI NOIR CAMERA BOARD - RASPBERRY-PI"))
*	**Female** to **Female** jumper wires, at least 3 (try [Pimoroni](http://shop.pimoroni.com/collections/components "Components - Pimoroni"))
*	220 Ohm Resistor, get several in case of breakages (try [Pimoroni](http://shop.pimoroni.com/collections/components "Components - Pimoroni"))
*	Infrared LED 5mm 890nm, get several in case of breakages (try [RS](http://uk.rs-online.com/web/p/ir-leds/6997663/ "Buy IR LEDs Infrared LED 5mm 890nm"))
* Bird Box (try [B&Q](http://www.diy.com/nav/garden/pet-bird-care/bird-care/nesting_boxes/Gardman-Wild-Bird-Nest-Box-9374965 "Gardman Wild Bird Nest Box"))

##Optional extras
If you want to be able to turn the Infrared LED on and off in code.
* ULN2003 Transistor Array (try [RS](http://uk.rs-online.com/web/p/darlington-transistors/6868209 "Buy Darlington Transistors ULN2003"))
* Breadboard (try [Pimoroni](http://shop.pimoroni.com/products/solderless-breadboard-830-point "Solderless Breadboard - 830 point - Pimoroni"))
*	**Male** to **Female** jumper wires, at least 3 (try [Pimoroni](http://shop.pimoroni.com/collections/components "Components - Pimoroni"))

##Introduction

To begin with pupils should appreciate that garden birds are very choosy about where they build their nest.  The bird box will need to be located out of any predator's reach, away from any prevailing winds and nowhere near a bird table or feeder.

Once a bird has moved in the box must not be disturbed until they have finished breeding (usually between October and January in the UK).  If something goes wrong you can't just open the box and fiddle with your wires or adjust the camera as this will traumatise the birds and could cause eggs or hatchlings to be abandoned.

A requirement of the camera is to see the birds in total darkness.  A light inside the bird box could attract insects and predators and therefore no birds would chose it as a nesting site.  It is possible though to illuminate the inside of the bird box with a kind of light that is invisible to animals and humans but *is* visible to a camera. This is commonly known as night vision.  Night vision works by using a spectrum of light called [Infrared](http://en.wikipedia.org/wiki/Infrared "Infrared - Wikipedia, the free encyclopedia") which has a longer wavelength than visible light.  Notice that IR is to the right hand side of the visible spectrum of light below.

![image](./images/spectrum.jpg "Electromagnetic spectrum")

Take this night vision surveillance camera below for example.  Around the camera lens there are lots of infrared LEDs (light emitting diodes).  These emit infrared light which will then bounce off various objects and return to the camera lens allowing it to create an image.

![image](./images/surveillance.jpg "Surveillance camera")

The image will look black and white (greyscale) though because there are no wavelengths of light from the visible spectrum being detected.  However a black and white image is good enough to allow you to watch what is happening inside a bird box and it doesn't disturb or interfere with the birds in any way.

![image](./images/pinoirada.jpg "Pi NoIR camera")

Above is the special version of the Raspberry Pi camera board called Pi NoIR.  It's essentially identical the normal green camera but it has no infrared filter.  Meaning that it lets in infrared light.  This camera combined with an infra red light source will give you night vision.  It's also small and won't be too intrusive when mounted on the inside of a bird box.

## Step 1: Setting Up your Pi
First check that you have all the parts you need to get your Raspberry Pi set up and working.

- Raspberry Pi
- Micro USB power adapter
- An SD Card with Raspbian already set up through NOOBS
- USB Keyboard
- USB Mouse
- HDMI cable
- A Monitor or TV

**Activity Checklist**

1.	Place the SD card into the slot of your Raspberry Pi. It will only fit one way so be careful not to break the card. 
2.	Next connect the HDMI cable from the monitor (or TV) to the HDMI port on the Pi and turn on your monitor. 
3.	Plug the USB keyboard and mouse into the USB slots on the Pi.
4.	Plug in the micro USB power supply and you should see some text appear on your screen.
5.  When prompted to login type:

    ```
    Login: pi
    Password: raspberry
    ```

##Step 2: Setting up the Camera Board

Firstly set up the Pi NoIR camera board without touching the bird box, test it first and we'll come to putting everything into the bird box later on.  Follow the official instructions [here](http://www.raspberrypi.org/camera "Camera | Raspberry Pi") and stop once you have successfully used a few of the example commands.

If you have not done so already you can test the camera video preview using the following command.

`raspivid -t 0`

You'll notice that everything looks a little strange.  This is because you're looking at a combination of visible light and infrared light.  A quick test is to turn the lights off and aim a TV remote control at your face (just press the buttons).  You should see your face illuminated in the darkness!

Press `Ctrl - C` when you want to exit.

##Step 3: Wire up the Infrared LED

The intention is to have a single Infrared LED illuminating the inside of the bird box to allow the Pi NoIR camera to see.  The LED is essentially identical to the ones found inside TV remote controls however we need to keep it on constantly to facilitate the live stream.

First check that you have all the required parts to do this.
* **Female** to **Female** jumper wires, at least 3
* 220 Ohm Resistor
* Infrared LED 5mm 890nm

