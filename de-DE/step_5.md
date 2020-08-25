## Pi NoIR einrichten

Richten Sie zunächst das Pi NoIR-Kameramodul ein und testen Sie es, ohne es an der Vogelbox anzubringen. Wir werden später auf diesen Teil zurückkommen. Folge den Anweisungen [hier](http://www.raspberrypi.org/camera) und stoppe, sobald du einige der Beispielbefehle erfolgreich verwendet hast.

Wenn du dies noch nicht getan hast, kannst du die Videovorschau der Kamera mit dem folgenden Befehl testen:

```bash
raspivid -t 0
```

Du wirst feststellen, dass alles etwas seltsam aussieht. Dies liegt daran, dass du eine Kombination aus sichtbarem Licht und Infrarotlicht betrachtest. Ein schneller Test besteht darin, das Licht auszuschalten, dann eine TV-Fernbedienung auf dein Gesicht zu richten und die Tasten zu drücken. Du solltest dein Gesicht in der Dunkelheit beleuchtet sehen.

Drücke `Strg + C.` wenn du die Vorschau beenden möchtest.

