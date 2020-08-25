## Streaming mit FFmpeg

Öffne ein Terminalfenster und mit nur einem Befehl kannst du mit dem Streaming zu YouTube beginnen. Du musst den `<key goes here>` Teil des Befehls entfernen und ihn durch deinen von YouTube kopierten Schlüssel ersetzen:

``` bash
raspivid -o - -t 0 -w 1280 -h 720 -fps 25 -b 4000000 -g 50 | ffmpeg -re -ar 44100 -ac 2 -acodec pcm_s16le -f s16le -ac 2 -i /dev/zero -f h264 -i - -vcodec copy -acodec aac -ab 128k -g 50 -strict experimental -f flv rtmp://a.rtmp.youtube.com/live2/<key goes here>
```

Es ist nie eine gute Idee, Befehle aus dem Internet zu kopieren und in ein Terminalfenster einzufügen ohne zu verstehen, was du eingibst. Lass es uns also ein wenig aufschlüsseln. Die erste Hälfte des Befehls bietet folgende Optionen:

- `raspivid -o -` weist den Raspberry Pi an, mit der Videoaufnahme zu beginnen.
- `-t 0` ist eine Option, um die Aufnahme für immer fortzusetzen.
- `-w 1280 -h 720` legt die Breite und Höhe des Videos in Pixeln fest.
- `-fps 25` stellt die Bildrate auf 25 Bilder pro Sekunde ein.
- `-b 4000000` stellt die Bitrate (die Geschwindigkeit der Datenübertragung) auf 4 Mbit/s ein.
- `-g 50` legt die Schlüsselbildrate fest. So wird alle 50 Bilder ein vollständiges Bild aufgenommen, während die Bilder dazwischen komprimiert werden.

Die zweite Hälfte des Befehls dient zum Streamen. Das `|` Symbol nimmt die Daten von `raspivid` und übergibt sie an `ffmpeg`.

- Das `-re` Flag weist FFmpeg an, dieselbe Bildrate zu verwenden, die von der Kamera aufgenommen wurde.
- `-ar 44100 -ac 2 -acodec pcm_s16le -f s16le -ac 2 -i /dev/zero`, `-acodec aac -ab 128k` und `-strict experimental` erstellt einen stillen Audiostream, da YouTube Videos mit Audio benötigt.
- `-f h264` und `-f flv` sind die Codecs, die FFmpeg von der Pi-Kamera empfängt und für die Ausgabe, die an YouTube gesendet wird.
- Die allerletzte Option sind deine persönlichen Streaming-Daten für YouTube.

