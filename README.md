
# VHS Video Tutorial

## VHS-Rekorder Anschließen
Zur Anbindung des VHS-Rekorders an den PC sind folgende Schritte notwendig:

1) Video-Grabber anschließen via USB
2) Scart-Kabel anschließen (Ton: Rot+Weiß, Video: Gelb, kein S-Video)
3) Info: Grabber-Treiber ist auf Ubuntu bereits vorinstalliert, keine Setup nötig

## Anzeigesoftware Installieren
Zum Abspielen und Aufzeichnen von VHS-Videos wird der VLC Media Player empfohlen.
Er kann unter Ubuntu mit folgende Befehlen installiert werden:

```sh
# install the VLC media player
sudo apt-get update && sudo apt-get install -y vlc

# see the official Ubuntu documentation:
# https://wiki.ubuntuusers.de/VLC/
```

## Video Abspielen
Zum Abspielen von VHS-Videos müssen folgende Einstellungne vorgenommen werden:

1) VLC Player öffnen
2) Media -> Open Capture Device
3) Folgende Einstellungen verwenden und den Vorgang mit 'Play' abschließen

```text
Device: Video Camera

Device Name: /dev/video0
Audio Device Name: hw:1,0

Video Standard: PAL
```

Info: Das Abspielen des Videos muss am Videorekorder manuell vorgenommen werden.
      VLC Media Player zeigt nur die Signale an, die der VHS-Rekorder ausgibt.

## Video Aufzeichnen
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
Aufnahme zu starten und erst danach das Videos über den VHS-Rekorder abzuspielen,
sodass das kompletten Video aufgezeichnet wird. Und natürlich sollte man auch
die Videokassette zurückspulen, bevor man aufzeichnet.

## Getestete Umgebung / Geräte

```text
OS: Ubuntu 20.04
VLC: 3.0.9.2
Grabber: mumbi (muss zum Linux-Treiber kompatibel sein)
VHS-Rekorder: Panasonic NV-FS200EG
```
