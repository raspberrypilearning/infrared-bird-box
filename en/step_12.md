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

- The `-re` flag tells FFmpeg to use the same frame rate as captured by the camera.
- `-ar 44100 -ac 2 -acodec pcm_s16le -f s16le -ac 2 -i /dev/zero`, `-acodec aac -ab 128k` and `-strict experimental` creates a silent audio stream, as YouTube needs audio to accompany its videos.
- `-f h264` and `-f flv` are the codecs FFmpeg is receiving from the PiCamera and the output it's sending to YouTube.
- The very last option is just your personal streaming details for YouTube.

