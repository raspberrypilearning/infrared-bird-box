## VNC setup on the Raspberry Pi

- First, you'll need to get the RealVNC server for your Raspberry Pi. You can download the **deb** package [here](https://github.com/RealVNC/raspi-preview/releases/download/5.3.1.18206/VNC-Server-5.3.1-raspi-alpha1.deb).
  - To install the package, open a terminal (**Ctrl + Alt + T**) and type the following command in the directory the deb package was downloaded to:

  ``` bash
  sudo dpkg -i VNC-Server-5.3.1-raspi-alpha1.deb
  ```

- You'll need a license key for the server, but don't worry: these are completely free. On the [RealVNC website](https://www.realvnc.com/purchase/activate/), you can fill in your details and obtain your free license key.
- Next, you need to apply the license key. This is again done in a terminal window with the following command:

  ``` bash
  sudo vnclicense -add <your-license-key-here->
  ```

- It's a good idea to find the IP address of your Pi. Be warned, though: this can change when it disconnects and reconnects to your network, although most networks will let the Raspberry Pi retain the same IP address for quite some time. To find your IP address, you can hover your mouse over the network icon in the top-left of the screen, or alternatively use the following command in the terminal:

  ``` bash
  hostname -I
  ```

- The next command will start your VNC server each time the Raspberry Pi is started. Again, it needs to be typed into a terminal window:

  ``` bash
  sudo systemctl enable vncserver-x11-serviced.service
  ```

- On your Windows, MacOS, or Linux computer, you can now take control of your Raspberry Pi. You'll need a VNC viewer, and 

