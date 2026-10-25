# lin-media

### Scaner

xsane ... scanovani ze scaneru, videa atd. - vyuziva ,a href="http://www.sane-project.org|SANE]] (Scanner Access Now Easy)  
sane-find-scanner ... najde USB scannery  
scanimage -d 'smfp:usb;04e8;3469;ZF5RB8KG1F00KNZ' --page-format A4 --resolution=300 --format=tiff -b ... nascanuje obrazek do tiffu  
xsane 'smfp:net;10.0.0.15' ... graficke scanovani, sitove spojeni s Samsung M2070  
convert out1.tif -resize 50% prihlaska2.png ... zkonvertuje a zmenisi obrazek  
convert *png prihlaska.pdf ... vytvori pdf  

### Multimedia

[Inspirace jak stahovat multimedia](http://blog.root.cz/nekolikero-postrehu-z-pc-sveta/jak-stahnout-multimedialni-obsah-z-internetu/)  
/proc/asound/cards  
alsamixer ... zesilovani, zeslabovani zvuku  
aplay aaa.wav ... prehraje a.wav  
aplay -L ... vylistuje vsechny PCM  
aplay -l .. vylistuje vsechny zarizeni, co mohou vydavat zvuk  
aplay -vv -D front:CARD=Intel,DEV=0 /usr/share/sounds/ekiga/ring.wav  
aplay -D plug:surround51 chan-ad.wav - (ftp://ling.ll.hawaii.edu/pub/greg/Surround-SDL-testfiles.tgs) test surround zvuku  
arecord -l ... seznam zarizeni na porizovani zvuku (input zarizeni)  
arecord -f cd - | aplay - ... preposilani mikrofonu na vystup  
arecord -f cd - | tee output.wav | aplay - ... preposilani mikrofonu na vystup, zaroven nahravani  
ffmpeg -f alsa -i hw:0,0 -t 30 out.wav ... zaznam zvuku ze zarizeni 0,0 (z arecord -l) po dobu 30 sekund do wav souboru  
[ffmpeg](https://trac.ffmpeg.org/wiki/Capture/ALSA) -f alsa -ac 1 -ar 44100  -i default:CARD=U0x46d0x809 -t 30 out.wav ... zaznam ze zarizeni (z arecord -L - ID zarizeni nezavisle na rebootu), channel 1, rate 44100 hz  
modprobe snd-aloop pcm_substreams=1 ... nahrani modulu na nahravani zvuku z aplikace (loopback zarizeni), vyzaduje upravu /etc/asound.conf  
fmpeg -f alsa -ac 2 -ar 44100 -i hw:Loopback,1,0 out.wav ... zaznam z loopback zarizeni (z aplikace)  
lsmod | grep snd  
lame input_file.wav output_file.mp3 ... prevede wav do mp3  
lame input.wav -b 256 --tt "song title" --ta "artist" output.mp3 ... prevede do mp3 v kvalite 265 Mbps a nastavi ID tagy  
[mplayer](http://linux.tosovsky.info/exec.php/show=mplayer2) -cdrom-device /dev/sr0 -cache 4096 -ao alsa:noblock:device=hw=0 cdda://.  
play a.wav ... prehraje soubor wav  
record a.wav ... nahrava z mikrofonu do a.wav  
pulseaudio - nutno dat pozor na prava /dev/snd/control??  
pulseaudio --log-target=syslog --system -D --disallow-exit ... restart demonu  
paman ... Pulse Audio Manager  
pavucontrol ... ovladaci padal pro Pulseaudio  
pactl load-module module-loopback latency_msec=1 ... (vyzaduje balicek pavucontrol) aktivuje posilani vstupu mikrofonu primo do vystupu  
pactl unload-module module-loopback ... deaktivuje preposilani mikrofonu na vystup  
pavumeter ... meri vykon repraku  
parec ... nahravani zvuku  
pacmd list-device ... vykonani Pulseaudio prikazu: ukaz moduly  
pacmd help ... seznam prikazu  
sox infile.aiff -r 44100 -w -c 2 outfile.wav ... prevede aiff do wav  

### Video

[/etc/mplayer/mplayer.conf](http://how-to.wikia.com/wiki/How_to_configure_MPlayer)  
mplayer mms://63.251.167.32/theriversidechurch ... prehravani streamoveho videa  
mplayer -ao pcm -aofile output.wav infile.wma ... konverze wma -&gt; wav  
mplayer /usr/share/sounds/purple/receive.wav  -volume 100 -softvol -softvol-max 1000 -ao pcm:file=a.wav ... zasileni zvuku a ulozeni audia do souboru  
mplayer dvd://5 -dvd-device . -vf cropdetect ... detekce oriznuti obrazu pro zkopirovane DVD do soucasneho adresare  
[mencoder](http://man.cx/mencoder(1)/cs) dvd://5 -chapter 2-2 ... prekodovani hudby/videa  
mencoder -ovc xvid -oac mp3lame -xvidencopts fixed_quant=5 -lameopts cbr:br=128:aq=1 -aid 128 -vf crop=672:560:20:8 -chapter 7-7 -o output.avi dvd://5 ... Konverze 7 kapitoly DVD to avi-xvid + mp3 zvuk  
mencoder dvd://5 -vf crop=672:560:20:8 -ovc xvid -xvidencopts bvhq=1:chroma_opt:quant_type=mpeg:bitrate=658:pass=1 -aid 128 -oac copy -o /dev/null -chapter 5-5 ... zapis toku dat pro 2 krokove kodovani  
mencoder dvd://5 -vf crop=672:560:20:8 -ovc xvid -xvidencopts bvhq=1:chroma_opt:quant_type=mpeg:bitrate=658:pass=2 -aid 128 -oac mp3lame -lameopts br=128:cbr:vol=0 -chapter 5-5 -o VIDEO.avi ... 2 krok - prekodovani 5. kapitoly DVD do mpeg xvid avi souboru  
tcprobe -i jmeno_filmu.avi ... zjisti, jakym kodekem byl film zakodovan (balicek transcode)  
ogle ... DVD prehravac  
ffmpeg -init_hw_device  list ... seznam vsech hardware zarizeni ktere podporuje toto ffmpeg  
ffmpeg  -hwaccels ... seznamm akceleracnich zarizeni  
ffmpeg -sample_fmts ... seznam samplovacich formatu  
ffmpeg -bsfs ... seznam bitstreamovych filtru  
ffmpeg -codecs ... seznam dekoderu  
ffmpeg -formats ... seznam formatu  
ffmpeg -filters ... seznam filtru  
ffmpeg -protocols ... seznam podporovanych protokolu  
ffmpeg -devices ... seznam podporovanych zarizeni  
ffmpeg -sources v4l2 ... seznam zdrojovych zarizeni pro v4l2 zarizeni (z -devices)  
ffmpeg -f v4l2 -list_formats all -i /dev/video0 ... seznam podporovanych formatu pro dane zarizeni  
[ffmpeg](https://ffmpeg.org/ffmpeg.html) -video_size 1024x768 -framerate 25 -f x11grab -i :0.0+100,200 output.mp4 ... zaznamenani obrazovky do video souboru  
ffmpeg -video_size 1024x768 -framerate 25 -f x11grab -i :0.0+100,200 -f alsa -ac 2 -i hw:0 output.mkv ... zaznamenani obrazovky i se zvukem (alsa driver)  
ffmpeg -video_size 1024x768 -framerate 25 -f x11grab -i :0.0+100,200 -f pulse -ac 2 -i default output.mkv ... zaznamenani obrazovky se zvukem (pulse driver)  
ffmpeg -video_size 1920x1080 -framerate 30 -f x11grab -i :0.0 -c:v libx264 -crf 0 -preset ultrafast output.mkv ... bezstratove kodovani (zadna komprese, velky soubor)  
ffmpeg -i output.mkv -c:v libx264 -crf 0 -preset veryslow output-smaller.mkv ... prekodovani na mensi vystup (pomale)  
[http://4youngpadawans.com/stream-camera-video-and-audio-with-ffmpeg/](http://4youngpadawans.com/stream-camera-video-and-audio-with-ffmpeg/) ... streamovani a sledovani videa  
[https://wiki.archlinux.org/index.php/FFmpeg#Recording_webcam](https://wiki.archlinux.org/index.php/FFmpeg#Recording_webcam) ... hodne pouziti ffmpeg  

##### Streamovani

sudo apt install libnginx-mod-rtmp

na konec /etc/nginx/nginx.conf pridat:

```
rtmp {
    server {
            listen 1935;
            chunk_size 4096;
            application live
    {
        live on;
                    record off;
        hls on;
        hls_path /tmp/hls;
        hls_fragment 12s;
    }
    }
}
```

ffmpeg -f v4l2 -framerate 10 -i /dev/video0 -c:v libx264 -crf 0 -preset ultrafast -b:v 128k -an -threads 0 -tune zerolatency -s 1028x768 -r 10 -f flv rtmp://10.0.0.4/live/test ... streamovani kamery  
ffmpeg -s 1680x1050 -r 10 -f x11grab -i :0.0 -c:v libx264 -crf 0 -preset ultrafast -b:v 128k -an -threads 0 -tune zerolatency -s 1028x768 -r 10 -f flv rtmp://10.0.0.4/live/test ... streamovani obrazovky  
rtmp://10.0.0.4/live/test ... link z Browseru, otevre se prehravacem

```
rtmp {
    server {
        listen 1935;
        chunk_size 8192;
        application vod {
            play /usr/local/nginx/rtmp;
        }
    }
}
```

a nahraje se do /usr/local/nginx/rtmp mp4 soubory. Prehrava se pak pomoci url: rtmp://10.0.0.4/vod/file_example_MP4_640_3MG.mp4 pro video file_example_MP4_640_3MG.mp4  
### Kamera

v4l2-ctl --list-devices ... seznam zarizeni asociovanych s kamerou  
v4l2-ctl -L ... zobrazi nastaveni obrazu kamery  
v4l2-ctl -c brightness=0 ... zmena nastaveni jasu  
ffmpeg -f v4l2 -list_formats all -i /dev/video0 ... podporovane formatypro zarizeni kamery  
ffmpeg -f v4l2 -framerate 25 -video_size 640x480 -i /dev/video0 output.mkv ... zaznam z kamery do souboru  
[fakecam](https://snapcraft.io/fakecam) ... virtualni kamera, kde se da menit pozadi  
### CD

cdda2wav -JD /dev/cdrom ... vylistuje stopy z CD  
cdda2wav -D /dev/cdrom -B ... prevede stopy z CD na disk  
cdda2wav -D /dev/cdrom -t 2 file.wav ... prevede 2 stopu do souboru  
cdrdao copy ... zkopiruje audio CD na jine CD  
cdrdao read-cd   --driver generic-mmc audiocd.toc ... cdrdao copy tremi kroky - zkopiruje na disk  
cdrdao read-cddb --driver generic-mmc audiocd.toc ... overi s CDDB  
cdrdao write  --driver generic-mmc audiocd.toc ... zapise na CDR  
cdplay ... prehravani CD  

### Zvuk

Mixxx ... Nastroj pro mixovani, DJ, vysilani radia atd.  
Audacity ... nahravani, editovani, efekty a prace se zvukem ve zvukovem soubory
