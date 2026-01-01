## Building PolyVGet-ffmpeg

This modified version uses ffmpeg's H264 decoder to read and x264 to write the video data. Audio is just copied over. Everything else has been disabled to reduce file size.

### Ubuntu
x264 doesn't need to be modified so install it via:
```
sudo apt install libx264-dev
```

Build ffmpeg:
```
git clone https://github.com/DevLARLEY/PolyVGet-ffmpeg.git
cd PolyVGet-ffmpeg
./configure \
  --enable-gpl \
  --enable-libx264 \
  --enable-static \
  --disable-shared \
  --extra-ldflags="-static" \
  --pkg-config-flags="--static" \
  --disable-everything \
  --enable-decoder=h264,aac \
  --enable-encoder=libx264 \
  --enable-demuxer=mpegts \
  --enable-muxer=mpegts \
  --enable-parser=h264,aac \
  --enable-protocol=file \
  --enable-bsf=h264_mp4toannexb,aac_adtstoasc
make -j$(nproc)
```

### Windows
Install MSYS2 and open the MINGW64 shell. 

Build x264:
```
git clone https://code.videolan.org/videolan/x264.git
cd x264
./configure --prefix=/mingw64 --enable-static
make -j$(nproc)
make install
```

Build ffmpeg (same as Ubuntu)
