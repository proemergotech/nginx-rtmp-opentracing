# docker-nginx-rtmp
A Dockerfile installing NGINX, nginx-rtmp-module and FFmpeg from source with
default settings for HLS live streaming. Built on Alpine Linux.

* Nginx 1.13.3 (compiled from source)
* nginx-rtmp-module 1.2.0 (compiled from source)
* lua-nginx-module 0.10.8 (compiled from source)
* ffmpeg 3.3.3 (compiled from source)
* Default HLS settings (See: [nginx.conf](nginx.conf))
* LuaJIT 2.0.5 (compiled from source)
* luarocks 2.4.2 (compiled from source)
* OpenResty 1.11.2.3 (compiled from source)

[![Docker Stars](https://img.shields.io/docker/stars/shakahl/docker-alpine-nginx-rtmp.svg)](https://hub.docker.com/r/shakahl/docker-alpine-nginx-rtmp/)
[![Docker Pulls](https://img.shields.io/docker/pulls/shakahl/docker-alpine-nginx-rtmp.svg)](https://hub.docker.com/r/shakahl/docker-alpine-nginx-rtmp/)
[![Docker Automated build](https://img.shields.io/docker/automated/shakahl/docker-alpine-nginx-rtmp.svg)](https://hub.docker.com/r/shakahl/docker-alpine-nginx-rtmp/builds/)
[![Build Status](https://travis-ci.org/shakahl/docker-alpine-nginx-rtmp.svg?branch=master)](https://travis-ci.org/shakahl/docker-alpine-nginx-rtmp)

## Usage

### Server
* Pull docker image and run:
```
docker pull shakahl/docker-alpine-nginx-rtmp
docker run -it -p 1935:1935 -p 8080:80 --rm shakahl/docker-alpine-nginx-rtmp
```
or 

* Build and run container from source:
```
docker build -t docker-alpine-nginx-rtmp .
docker run -it -p 1935:1935 -p 8080:80 --rm docker-alpine-nginx-rtmp
```

* Stream live content to:
```
rtmp://<server ip>:1935/stream/$STREAM_NAME
```

### OBS Configuration
* Stream Type: `Custom Streaming Server`
* URL: `rtmp://localhost:1935/stream`
* Stream Key: `hello`

### Watch Stream
* In Safari, VLC or any HLS player, open:
```
http://<server ip>:8080/live/$STREAM_NAME.m3u8
```
* Example: `http://localhost:8080/live/hello`


### FFmpeg Build
```
ffmpeg version 3.3.1 Copyright (c) 2000-2016 the FFmpeg developers
  built with gcc 5.3.0 (Alpine 5.3.0)
  configuration: --enable-version3 --enable-gpl --enable-nonfree --enable-small --enable-libmp3lame --enable-libx264 --enable-libx265 --enable-libvpx --enable-libtheora --enable-libvorbis --enable-libopus --enable-libfdk-aac --enable-libass --enable-libwebp --enable-librtmp --enable-postproc --enable-avresample --enable-libfreetype --enable-openssl --disable-debug
  libavutil      55. 17.103 / 55. 17.103
  libavcodec     57. 24.102 / 57. 24.102
  libavformat    57. 25.100 / 57. 25.100
  libavdevice    57.  0.101 / 57.  0.101
  libavfilter     6. 31.100 /  6. 31.100
  libavresample   3.  0.  0 /  3.  0.  0
  libswscale      4.  0.100 /  4.  0.100
  libswresample   2.  0.101 /  2.  0.101
  libpostproc    54.  0.100 / 54.  0.100

  configuration:
    --enable-version3
    --enable-gpl
    --enable-nonfree
    --enable-small
    --enable-libmp3lame
    --enable-libx264
    --enable-libx265
    --enable-libvpx
    --enable-libtheora
    --enable-libvorbis
    --enable-libopus
    --enable-libfdk-aac
    --enable-libass
    --enable-libwebp
    --enable-librtmp
    --enable-postproc
    --enable-avresample
    --enable-libfreetype
    --enable-openssl
    --disable-debug
```

## Resources
* https://alpinelinux.org/
* http://nginx.org
* https://github.com/arut/nginx-rtmp-module
* https://www.ffmpeg.org
* https://obsproject.com

## Credits

This project is based on [alfg/docker-nginx-rtmp](https://github.com/alfg/docker-nginx-rtmp)
