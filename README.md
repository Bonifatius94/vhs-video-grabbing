
# VHS Video Tutorial

## VHS-Rekorder anschließen
Zur Anbindung des VHS-Rekorders an den PC sind folgende Schritte notwendig:

1) Video-Grabber anschließen via USB
2) Scart-Kabel anschließen (Ton: Rot+Weiß, Video: Gelb, kein S-Video)
3) Info: Grabber-Treiber ist auf Ubuntu bereits vorinstalliert, keine Setup nötig

## Anzeigesoftware VCL Media Player installieren
Zum Abspielen und Aufzeichnen von VHS-Videos wird der VLC Media Player empfohlen.
Er kann unter Ubuntu mit folgenden Befehlen installiert werden:

```sh
# install the VLC media player
sudo apt-get update && sudo apt-get install -y vlc

# see the official Ubuntu documentation:
# https://wiki.ubuntuusers.de/VLC/
```

## Alternativ: Anzeigesoftware MPlayer installieren
Ein alternatives Programm zum Abspielen und Aufzeichnen von VHS-Videos stellt der
MPlayer dar. Er kann unter Ubuntu mit folgenden Befehlen installiert werden:

```sh
# install the MPlayer software
sudo apt-get update && sudo apt-get install -y mplayer mplayer-gui

# fix the style config, in case you encounter MPlayer style page errors
# see: https://askubuntu.com/questions/943068/error-in-skin-config-file-with-mplayer
sudo apt-get update && sudo apt-get install -y imagemagick
cd /usr/share/mplayer/skins/default; for FILE in *.png; do sudo convert $FILE -define png:format=png24 $FILE; done

# see the official Ubuntu documentation:
# https://wiki.ubuntuusers.de/MPlayer/
```

## Video mit VLC Media Player abspielen

### Video abspielen (kein S-Video)
Zum Abspielen von VHS-Videos müssen folgende Einstellungen vorgenommen werden:

1) VLC Player öffnen
2) Media -> Open Capture Device
3) Folgende Einstellungen verwenden

```text
Device: Video Camera

Device Name: /dev/video0
Audio Device Name: hw:1,0

Video Standard: PAL
```

4) Unter "Advanced Options" folgende Einstellung zusätzliche vornehmen (nur für S-Video):

```text
Input: 4
```

Info: Das Abspielen des Videos muss am Videorekorder manuell vorgenommen werden.
      VLC Media Player zeigt nur die Signale an, die der VHS-Rekorder ausgibt.

### Video aufzeichnen
Das Aufzeichnen von Videos funktioniert ähnlich wie das Abspielen von Videos.
Hier werden dieselben Einstellungen wie zuvor vorgenommen, allerdings wird beim
Abschließen des Konfigurationsdialogs nicht mit 'Play' sondern mit 'Convert'
bestätigt. Danach öffnet sich ein weiterer Dialog, über den man Einstellungen
treffen kann, in welche Datei geschrieben werden soll, welche Video-Kodierung
verwendet werden soll usw. Hierbei werden folgende Einstellungen empfohlen:

```text
Source: v4l2://dev/video0

Convert (set bullet-point)
Display the Output: enable if you want, may be lagging a lot
...
Profile: Video - H.264  MP3 (MP4)

Destination File: use 'Browse' to choose a proper file path
```

Nachdem die gewünschten Einstellungen gewählt wurden, kann mit der Schaltfläche
'Start' die Aufzeichnung gestartet werden. Hierbei ist es ratsam, zuerst die
Aufnahme zu starten und erst danach das Video über den VHS-Rekorder abzuspielen,
sodass das komplette Video aufgezeichnet wird. Und natürlich sollte man auch
die Videokassette zurückspulen, bevor man aufzeichnet.

### Video Abspielen / Aufzeichnen via Kommandozeile
Das Abspielen und Aufzeichnen von VHS-Videos kann auch per Kommandozeile
gestartet werden mithilfe folgender Kommandos:

```sh
# play a VHS video via s-video signal (channel 4)
cvlc "v4l2:///dev/video0:input=4:width=720:height=576:norm=PAL:input-slave=alsa://plughw:1,0"
# TODO: make the audio work here ...
```

## Video Abspielen mit MPlayer (S-Video)
Für das Abspielen von S-Video bitte folgendes Kommando verwenden:

```sh
# use /dev/video0 device, video channel 4, audio via ALSA hw:1,0
mplayer tv:// -tv driver=v4l2:width=720:height=576:outfmt=uyvy:device=/dev/video0:input=4:norm=PAL:fps=25:alsa:amode=1:forcechan=2:audiorate=48000:adevice=plughw.1,0:forceaudio:immediatemode=0 -ao sdl -vo sdl
```

## Getestete Umgebung / Geräte

```text
OS: Ubuntu 20.04
VLC: 3.0.9.2
Grabber: mumbi (muss zum Linux-Treiber kompatibel sein)
VHS-Rekorder: Panasonic NV-FS200EG
```

