## VNC-Setup auf dem Raspberry Pi

- Zunächst musst du den RealVNC-Server für deinen Raspberry Pi herunterladen. Du kannst das **deb** Paket [hier](https://github.com/RealVNC/raspi-preview/releases/download/5.3.1.18206/VNC-Server-5.3.1-raspi-alpha1.deb) herunterladen.
  - Öffne zum Installieren des Pakets ein Terminalfenster (**Strg + Alt + T**) und gib den folgenden Befehl in das Verzeichnis ein, in das das Deb-Paket heruntergeladen wurde:

  ``` bash
  sudo dpkg -i VNC-Server-5.3.1-raspi-alpha1.deb
  ```

- Du benötigst einen Lizenzschlüssel für den Server, aber keine Sorge: der ist völlig kostenlos. Auf der [RealVNC-Website](https://www.realvnc.com/purchase/activate/) kannst du deine Daten eingeben und deinen kostenlosen Lizenzschlüssel erhalten.
- Als Nächstes musst du den Lizenzschlüssel hinzufügen. Dies erfolgt erneut in einem Terminalfenster mit dem folgenden Befehl:

  ``` bash
  sudo vnclicense -add <your-license-key-here->
  ```

- Es ist eine gute Idee, die IP-Adresse deines Pi zu finden. Sei jedoch gewarnt: diese kann sich ändern, wenn die Verbindung zu deinem Netzwerk getrennt und wieder hergestellt wird. In den meisten Netzwerken behält der Raspberry Pi jedoch für einige Zeit die gleiche IP-Adresse bei. Um deine IP-Adresse zu finden, kannst du mit der Maus über das Netzwerksymbol oben links auf dem Bildschirm fahren oder alternativ den folgenden Befehl im Terminal verwenden:

  ``` bash
  hostname -I
  ```

- Der nächste Befehl startet deinen VNC-Server jedes Mal, wenn der Raspberry Pi gestartet wird. Auch hier muss der Befehl in ein Terminalfenster eingegeben werden:

  ``` bash
  sudo systemctl enable vncserver-x11-serviced.service
  ```

- Auf deinem Windows-, MacOS- oder Linux-Computer kannst du jetzt die Kontrolle über deinen Raspberry Pi übernehmen. Du benötigst einen VNC-Viewer und 

