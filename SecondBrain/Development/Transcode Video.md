

## compile Handbrake with fdkaac

```bash
sudo apt-get install autoconf automake build-essential cmake git libass-dev libbz2-dev libfontconfig1-dev libfreetype6-dev libfribidi-dev libharfbuzz-dev libjansson-dev liblzma-dev libmp3lame-dev libogg-dev libopus-dev libsamplerate-dev libspeex-dev libtheora-dev libtool libtool-bin libvorbis-dev libx264-dev libxml2-dev m4 

make nasm patch pkg-config python tar yasm zlib1g-dev

sudo apt-get install intltool libappindicator-dev libdbus-glib-1-dev libglib2.0-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgtk-3-dev libgudev-1.0-dev libnotify-dev libwebkitgtk-3.0-dev

git clone https://github.com/HandBrake/HandBrake.git
cd HandBrake/
./configure --enable-fdk --launch-jobs=$(nproc) --launch
sudo make --directory=build install
```

## Downmix Sourround sound to stereo
#ffmpeg

```bash
# 5.1 to 2.0 FLAC

ffmpeg -i Der_Hauptmann_flac_t00.mkv -c:v copy -c:a flac -ac 2 -af "pan=stereo|FL < 1.0*FL + 0.7071*FC + 1.0*BL + 0.7071*LFE|FR < 1.0*FR + 0.7071*FC + 1.0*BR + 0.7071LFE" -sample_fmt s16 stereo.mkv

# 7.1 to 2.0 FLAC

ffmpeg -i MARVEL\'S_GUARDIANS_OF_THE_GALAXY_-_BLU-RAY_t00.mkv -c:v copy -c:a flac -ac 2 -af "pan=stereo|FL < 1.0*FL + 0.7071*FC + 1.0*BL + 1.0*SL + 0.7071*LFE|FR < 1.0*FR + 0.7071*FC + 1.0*BR + 1.0*SR + 0.7071*LFE" -sample_fmt s16 stereo.mkv

# 7.1 to 2.0 AAC

ffmpeg -i Star_Trek_Into_Darkness_t00.mkv -c:v copy -c:a libfdk_aac -b:a 512k -cutoff 20000 -ac 2 -af "pan=stereo|FL < 1.0*FL + 0.7071*FC + 1.0*BL + 1.0*SL + 0.7071*LFE|FR < 1.0*FR + 0.7071*FC + 1.0*BR + 1.0*SR + 0.7071*LFE"  stereo.mkv

# 5.1 -> flac
ffmpeg -i Star\ Trek\ Discovery\ Disc\ 1_t02.mkv -map 0:0 -map 0:1 -map 0:2 -c:v copy -c:a flac -ac 2 -af "pan=stereo|FL < 1.0*FL + 0.7071*FC + 1.0*BL + 0.7071*LFE|FR < 1.0*FR + 0.7071*FC + 1.0*BR + 0.7071LFE" -sample_fmt s16 -c:s copy e01-stereo-flac.mkv
```

Quellen:
- https://superuser.com/questions/852400/properly-downmix-5-1-to-stereo-using-ffmpeg#1048757
- https://forum.doom9.org/showthread.php?p=1600695#post1600695
- https://stackoverflow.com/questions/41420391/ffmpeg-flac-24-bit-96khz-to-16-bit-48khz