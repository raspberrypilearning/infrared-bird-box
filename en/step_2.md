## What you will need

### Hardware

* Raspberry Pi NOIR camera module
* 3 or more x Female-to-female jumper leads
* Some 220 Ohm 1% Resistors
* Some Infrared LEDs (5mm 890nm)

### Software

#### Software installation

You'll need to make sure you have the following packages installed to proceed with the workshop.

- ffmpeg

You'll need to be online to install packages.

First update and upgrade your system. Enter the following commands in to the terminal:

```bash
sudo apt-get update
sudo apt-get upgrade
```

Now install the packages you'll need:

```bash
sudo apt-get install ffmpeg
```

Test you have `ffmpeg` installed by entering `avconv` at the command line. You should see some information about the `avconv` tool. If you see the error

```
The program 'avconv' is currently not installed.
```

then make sure you enter the `ffmpeg` package properly by checking the command above.
