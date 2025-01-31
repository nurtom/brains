```bash
./ffmpeg -i /daten/home/developer/working_folder/video-processor/full-hd.mp4 -y -movflags +faststart -vf scale=640:360 -c:a aac -b:a 64k -c:v h264_nvenc -profile:v main -qmin 32 -qmax 37 -preset slow -bf 2 -g 125 -i_qfactor 1.1 -b_qfactor 1.25 -pix_fmt yuv420p /daten/home/developer/working_folder/video-processor/out360p.mp4
```

```bash
./ffmpeg -i /daten/home/developer/working_folder/video-processor/full-hd.mp4 -y -an -filter:v select='gt(scene,0.4)',showinfo -f null NUL
```

```bash
apt install nvidia-cuda-toolkit
```

- Install nvidia 470 driver: https://wiki.debian.org/NvidiaGraphicsDrivers#Version_470.103.01-2
- Add bullseye-backports as an additional new line to your /etc/apt/sources.list, for example:

```bash
#bullseye-backports
deb http://deb.debian.org/debian bullseye-backports main contrib non-free
```

Update the list of available packages, then we can install the nvidia-driver package, plus the necessary firmware, from the backports repository:

```bash
# apt update
# apt install -t bullseye-backports nvidia-driver firmware-misc-nonfree

#get latest nv-codec-headers
git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git
cd nv-codec-headers && sudo make install && cd –


#get ffmpeg
git clone https://git.ffmpeg.org/ffmpeg.git ffmpeg/
sudo apt-get install build-essential yasm cmake libtool libc6 libc6-dev unzip wget libnuma1 libnuma-dev
```

```bash
apt install libbluray-dev libbs2b-dev libcaca-dev libdc1394-dev libfribidi-dev libgme-dev libgsm1-dev libmp3lame-dev libopenjp2-7-dev libopenmpt-dev libopus-dev libpulse-dev librubberband-dev libshine-dev libsnappy-dev libsoxr-dev libssh-dev libspeex-dev libtheora-dev libtwolame-dev libvpx-dev libwebp-dev libx264-dev libx265-dev libxvidcore-dev libzmq5-dev libzvbi-dev libopenal-dev libomxil-dev libcdio-dev libcdio-paranoia-dev libsdl2-dev libchromaprint-dev frei0r-plugins-dev gnutls-dev ladspa-sdk-dev libiec61883-dev libass-dev
```

no: libopencv-dev

```bash
./configure --prefix=/usr --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu  --enable-nonfree --enable-cuda-nvcc --enable-libnpp --extra-cflags=-I/usr/local/cuda/include --extra-ldflags=-L/usr/local/cuda/lib64 --disable-static --enable-shared --enable-gpl --disable-stripping  --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio  --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmp3lame --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx265 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-omx --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394  --enable-libx264  --enable-chromaprint --enable-frei0r --enable-gnutls --enable-ladspa --enable-libass 
```

```bash
./configure --prefix=/usr --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu  --enable-nonfree --enable-cuda-nvcc --enable-libnpp --extra-cflags=-I/usr/local/cuda/include --extra-ldflags=-L/usr/local/cuda/lib64 --disable-shared --enable-static --enable-gpl --disable-stripping  --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio  --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmp3lame --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx265 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-omx --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394  --enable-libx264  --enable-chromaprint --enable-frei0r --enable-gnutls --enable-ladspa --enable-libass 
```

no: --enable-libflite --enable-libopencv  --enable-avisynth --enable-libiec61883

```bash
--extra-version=1+deb9u1  --prefix=/usr --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu  
```

```bash
make -j 4
sudo make install
```
