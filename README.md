# nginx-rtmp-opentracing
A Dockerfile installing Openresty based Nginx with the default Openresty modules, nginx-rtmp-module, Nginx Opentracing module with Jaeger tracer
and FFmpeg from source with default settings for HLS live streaming. Built on Alpine Linux.

* Openresty 1.13.6.1
* Nginx 1.13.6
* nginx-rtmp-module 1.2.1
* Opentracing C++ client 1.2.0
* Jaeger C++ client 0.2.0
* Nginx Opentracing module 0.2.1
* ffmpeg 3.4.2
* Default HLS settings (See: [nginx.conf](nginx.conf))

[![Docker Stars](https://img.shields.io/docker/stars/shakahl/nginx-rtmp-opentracing.svg)](https://hub.docker.com/r/shakahl/nginx-rtmp-opentracing/)
[![Docker Pulls](https://img.shields.io/docker/pulls/shakahl/nginx-rtmp-opentracing.svg)](https://hub.docker.com/r/shakahl/nginx-rtmp-opentracing/)
[![Docker Automated build](https://img.shields.io/docker/automated/shakahl/nginx-rtmp-opentracing.svg)](https://hub.docker.com/r/shakahl/nginx-rtmp-opentracing/builds/)
[![Build Status](https://travis-ci.org/shakahl/nginx-rtmp-opentracing.svg?branch=master)](https://travis-ci.org/shakahl/nginx-rtmp-opentracing)

## Usage

### Server
* Pull docker image and run:
```
docker pull proemergotech/nginx-rtmp-opentracing
docker run -it -p 1935:1935 -p 8080:80 --rm proemergotech/nginx-rtmp-opentracing
```
or 

* Build and run container from source:
```
docker build -t nginx-rtmp-opentracing .
docker run -it -p 1935:1935 -p 8080:80 --rm nginx-rtmp-opentracing
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
ffmpeg version 3.4.2 Copyright (c) 2000-2016 the FFmpeg developers
  built with gcc 6.3.0 (Alpine 6.3.0)
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
* https://openresty.org/en/
* http://nginx.org
* https://github.com/arut/nginx-rtmp-module
* https://github.com/opentracing-contrib/nginx-opentracing
* http://jaeger.readthedocs.io/en/latest/client_libraries/
* https://www.ffmpeg.org
* https://obsproject.com

## Credits

This project is based on [alfg/docker-nginx-rtmp](https://github.com/alfg/docker-nginx-rtmp)
