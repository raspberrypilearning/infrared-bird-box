# Infrared Bird Box - Part 2 

In this project, you will use a Raspberry Pi and a Pi NoIR Camera Module to allow you to observe nesting birds without disturbing them. This advanced worksheet covers how to stream the video you produce to the internet. 

## YouTube Setup

1. Go to [YouTube](https://www.youtube.com/), and sign in.
1. On the left-hand side of the screen you should see a menu with the **My Channel** option available:

  ![channel](images/channel.png)

1. In the middle of the screen you should see the **Video Manager** option:

  ![video manager](images/video-manager.png)

1. In the menu on the left you should see a **Live Streaming** option, and within that a **Stream now BETA** option:

  ![live stream](images/live-stream.png)

1. Scroll down to the bottom of the page, and you should see the **Encoder Setup** option:

  ![encoder setup](images/encoder-setup.png)
  
1. Within **Encoder Setup** there is a **Server URL** and a **Stream name/key**. The key will appear to be just a line of asterisks, until you click on the **Reveal** button. You need to keep the key secret, though, so make sure you don't share it online.

## Compile FFmpeg

Firstly, you need to install some software called [FFmpeg](http://www.ffmpeg.org/), which will continually stream the video data from the Camera Module to the web. Instructions are below.

**NOTE**: This step is going to take about two hours, since you have to [compile](http://en.wikipedia.org/wiki/Compiler) the program from its source code. The Raspbian FFmpeg package that can be installed using `apt-get` doesn't have the required `h264` video encoder support. You can just set the process going and do something else during this time; you'll also only need to do it once.

The part that takes two hours is the `make` command at the end of the list below. The `./configure` part takes a while too; just be patient. Enter the following commands to download, compile, and install FFmpeg:

```bash
cd /usr/src
sudo mkdir ffmpeg
sudo chown pi:users ffmpeg
git clone git://source.ffmpeg.org/ffmpeg.git ffmpeg
cd ffmpeg
./configure
make && sudo make install
```

You can now do something else until you see the command prompt reappear.

## Streaming with FFmpeg

Open a terminal window and then, with this single command, you can start streaming to YouTube. You'll need to remove the `<key goes here>` part of the command and replace it with your key copied from YouTube:

``` bash
raspivid -o - -t 0 -w 1280 -h 720 -fps 25 -b 4000000 -g 50 | ffmpeg -re -ar 44100 -ac 2 -acodec pcm_s16le -f s16le -ac 2 -i /dev/zero -f h264 -i - -vcodec copy -acodec aac -ab 128k -g 50 -strict experimental -f flv rtmp://a.rtmp.youtube.com/live2/<key goes here>
```

It's never a good idea to copy and paste commands from the internet into a terminal window without understanding what you're typing, so let's break it down a little. The first half of the command has the following options:

- `raspivid -o -` tells the Raspberry Pi to start capturing video.
- `-t 0` is an option to keep recording forever.
- `-w 1280 -h 720` sets the video's width and height in pixels.
- `-fps 25` set the frame rate to 25 frames per second.
- `-b 4000000` sets the bit rate (the speed of data transfer) to 4Mbps.
- `-g 50` sets the key frame rate. So a complete picture will be recorded every 50 frames, while the ones in between will be compressed.

The second half of the command is for streaming. The `|` symbol takes the data from `raspivid` and passes it to `ffmpeg`.

- The `-re` flag tells FFmpeg to use the same frame rate as captured by the Camera Module.
- `-ar 44100 -ac 2 -acodec pcm_s16le -f s16le -ac 2 -i /dev/zero`, `-acodec aac -ab 128k` and `-strict experimental` creates a silent audio stream, as YouTube needs audio to accompany its videos.
- `-f h264` and `-f flv` are the codecs FFmpeg is receiving from the Camera Module and the output it's sending to YouTube.
- The very last option is just your personal streaming details for YouTube.

## Viewing your stream

Once you have run the command, you can hop back over to YouTube and, after a minute or two, you should see your video being streamed for anyone to watch.

Remember: be careful about what content you place on the internet, especially in a public channel.

## Remote control

The last thing you should consider is being able to access the Raspberry Pi remotely from another computer, without having to have a keyboard, mouse, and monitor connected to it. Having these attached would be pretty inconvenient if the Pi is located somewhere outside, like up a tree.

The easiest way to remotely access the Pi is to use VNC. Instructions for working with VNC on the Raspberry Pi can be found in our [remote working guide](https://www.raspberrypi.org/learning/teachers-guide/remote/).


## What next?

- Wait for some birds to move in
- Tell the world about your bird box
- Share the YouTube channel URL on social media or with to your friends and family
