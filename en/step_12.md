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

