# Streaming video to the Internet

[Ustream](http://www.ustream.tv/) is one of the most popular live video streaming sites on the Internet. It's used by NASA to stream video from the [International Space Station](http://www.ustream.tv/channel/live-iss-stream) to all over the world. Websites like [Ustream](http://www.ustream.tv/), [YouTube Live](http://www.youtube.com/live), [Bambuser](http://bambuser.com/) and [justin.tv](http://www.justin.tv/) are known as *content distribution services*.

We need to use a service like this because you could potentially have thousands of people watching your bird box simultaneously. If you were to try and host that many viewers from your own Internet connection, your router would probably go into meltdown. There would simply not be enough upload [bandwidth](http://en.wikipedia.org/wiki/Bandwidth_%28computing%29).

With a content distribution service provider, you send your video content to them and they then host the connection to all the viewers. Therefore, you offload that bandwidth requirement from your own Internet connection *to them*. That way, you don't have to worry about how many people are concurrently watching the bird box or how much bandwidth is being used.

The only drawback is that there will be a delay on the video. For example, if you poked your finger into the bird box, you would only see it online 20 to 30 seconds later. Despite this, it will make a perfectly viable solution for sharing the bird box with the world.

## Compile FFmpeg

Firstly, you need to install some software called [FFmpeg](http://www.ffmpeg.org/) on the Raspberry Pi which will continually stream the video data from the camera board to the web. Instructions are below.

**NOTE:** This step is going to take about **two hours** since you have to [compile](http://en.wikipedia.org/wiki/Compiler) the program from its source code. The Raspbian FFmpeg package that can be installed using `apt-get` doesn't have the required `h264` video encoder support. You can just set the process going and do something else during this time; you'll also only need to do it once.

The part that takes two hours is the `make` command at the end of the list below. The `./configure` part takes a while too; just be patient. Enter the following commands to download, compile and install FFmpeg:

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

## Create a free Ustream account

If you have not done so already, go to [ustream.tv](http://www.ustream.tv/) on a PC or laptop and click `Sign Up`.

Enter your details to create an account for yourself. During the signup process you'll be asked to create a channel; try to think of an interesting name for it, so that people who find it will remember it easily.

Feel free to customise it; give your channel an avatar as well.

The account will be free and will do everything we need it to. However, after 30 days some adverts will show on the side of the page where your live video is; this is part of the Ustream business model. You can buy a pro account and get access to many more features, as well as disabling adverts; that isn't necessary for this project, though.

We need to copy two settings from your Ustream account to use on the Raspberry Pi: the *RTMP address* and the *stream key*. These two settings are needed by FFmpeg so that the data is streamed to the correct Ustream channel.

To find these two settings follow the steps below:

- Log in
- Select **Dashboard** from the top right menu
- Select **CHANNELS** from the left hand menu
- Select your channel
- Select **Broadcast Settings**
- Select **Encoder settings > View**

You should then see the screen below; however, the **RTMP URL** and **Stream Key** fields will contain text. Keep this page open for use in the next step.

![](images/ustream-remote-settings.png)

## Go live!

The intention is to stream the video content from the bird box to the Internet on a 24/7 basis. Considering that sometimes Internet servers can go down, it's a good idea to ensure that the Raspberry Pi will keep trying to send out the video stream if there is a problem.

To do that we can create a small shell script with a while loop; inside that loop is the command to start the stream. If something causes the stream command to go wrong and exit, the shell script will go around the loop and try the command again indefinitely.

On the Raspberry Pi let's create a script to do this. Enter the following command:

```bash
nano ~/ustream
```

Now copy and paste the code below, but replace `<rtmpurl>` and `<streamkey>` with the corresponding values from your own Ustream encoder settings page (see previous step):

```bash
#!/bin/bash
RTMP_URL=<rtmpurl>
STREAM_KEY=<streamkey>
while :
do
    raspivid -n -vf -hf -t 0 -w 960 -h 540 -fps 25 -b 500000 -o - | ffmpeg -i - -vcodec copy -an -metadata title="Streaming from raspberry pi camera" -f flv $RTMP_URL/$STREAM_KEY
    sleep 2
done
```

Press `Ctrl + O` then `Enter` to save and `Ctrl + X` to quit.

We're almost there. Enter the following command to make the shell script executable:

```bash
chmod +x ~/ustream
```

Now whenever you want to go live just use the following command:

```bash
~/ustream
```

You can view the live stream on a PC or laptop by going to the Ustream channel URL in a browser. This can be accessed using the ![](images/ustream-channel-icon.png) icon on the right of your channel name under **CHANNELS** in the Ustream dashboard. See the green square in the screen shot above.

When you have the video feed on screen, perform a test to see what the latency is like. Poke your finger inside the entrance of the bird box and time how long it takes to appear online. The URL in the browser address bar can now be sent to your friends over email, Facebook or Twitter and they should all be able to view what is happening in your bird box.

Press `Ctrl + C` twice when you want to shut the stream down.

## Remote control

The last thing you should consider is being able to remotely access the Raspberry Pi from another computer without having to have a keyboard, mouse and monitor connected to it. This would be pretty inconvenient if it's somewhere outside, up a tree for example.

You should familiarise yourself with SSH (Secure Shell Server). This is a technique that allows you to have the Raspberry Pi command prompt inside a window on another PC or Mac. As long as the other PC has network access to the Raspberry Pi, you can have full remote control.

The instructions [here](http://www.raspberrypi.org/documentation/remote-access/ssh/README.md) cover how to do this from Windows, OS X or Linux.

After you're comfortable with that you'll need a way to run `~/ustream` over SSH and then disconnect from the Pi, leaving it running. If you were to run `~/ustream` in an SSH window and then close that window, you wouldn't be able to get back to it to see if there was a problem. Ideally, you don't really want to keep an SSH window open at all times on another PC or Mac, so here is a simple way to solve this problem.

## Screen

Screen is a little utility that allows you to have multiple terminal sessions with only one SSH connection to the Pi. It's incredibly handy and once you've used it, you'll use it all the time.

It works like virtual command prompt. You can have as many of them as you want. When you start a screen you're automatically connected to it and can see what it shows. You can start a program and then disconnect from the screen but leave it running in the background. Later on you can come back and reconnect to the screen and see what has happened while you were away. Let's try it now.
 
Firstly, you'll need to install it as it doesn't come installed by default. You'll only need to do this once:

```bash
sudo apt-get install screen
```

Then, to start a new session enter the following command:

```bash
screen bash
```

This will now give you a blank session showing the command prompt. Enter the command below; this is the terminal equivalent of Task Manager in Windows:

```bash
top
```

We'll use this as our program to leave running in the background. Now press `Ctrl + A + D` to disconnect from the screen. You should be back at the previous command prompt. Now close the SSH window completely, wait a few seconds and re-connect.

To get back into and resume the screen session enter the following command:

```bash
screen -r
```

You should now be looking at `top` once again, you can see it's still running and has been the entire time you were disconnected. Press `Ctrl + C` to close `top`, and then you can type `exit` to close down the screen session.

We can now make the Raspberry Pi start a screen for the `~/ustream` script at boot time. That way if the bird box ever loses power, from a power cut for instance, it will reboot and start streaming video to the Internet automatically without any human intervention.

Enter the command below:

`sudo nano /etc/rc.local`

This file is a script which runs every time the Raspberry Pi boots up. At the end of the file you'll see `exit 0`, copy and paste the command below onto the previous line:

```bash
screen -S birdbox -dms birdbox /home/pi/ustream
```

Press `Ctrl + O` then `Enter` to save and `Ctrl + X` to quit.

Reboot now to test it.

```
sudo reboot
```

When the Raspberry Pi comes back up reload the Ustream channel URL on another PC and you should see the video feed. Remember there will be about a 20 to 30 second delay on what you see.

The screen session that we started automatically will be running as the *root* user so you can reconnect to us using the command below:

```bash
sudo screen -r
```

## What next?

- Wait for some birds to move in
- Tell the world about your bird box
- Post the Ustream channel URL on social media or email it to your friends and family