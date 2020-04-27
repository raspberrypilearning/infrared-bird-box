## Setting up the Pi NoIR

Firstly, set up the Pi NoIR camera module and test it, without fitting it to the bird box: we will come to that part later. Follow the instructions [here](http://www.raspberrypi.org/camera) and stop once you have successfully used a few of the example commands.

If you have not done so already, you can test the camera video preview using the following command:

```bash
raspivid -t 0
```

You'll notice that everything looks a little strange. This is because you're looking at a combination of visible light and infrared light. A quick test is to turn the lights off, and then aim a TV remote control at your face and press the buttons. You should see your face illuminated in the darkness.

Press `Ctrl + C` when you want to exit.

