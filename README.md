# nginx-rtmp-opentracing
A Dockerfile installing Openresty based Nginx with the default Openresty modules, nginx-rtmp-module, Nginx Opentracing module with Jaeger tracer
and FFmpeg from source with default settings for HLS live streaming and nvidia GPU support.

* Openresty 1.13.6.1
* Nginx 1.13.6
* nginx-rtmp-module 1.2.1
* Opentracing C++ client 1.5.0
* Jaeger C++ client 0.4.2
* Nginx Opentracing module 0.6.0
* ffmpeg 4.1
* Default HLS settings (See: [nginx.conf](nginx.conf))

[![Docker Stars](https://img.shields.io/docker/stars/proemergotech/nginx-rtmp-opentracing.svg)](https://hub.docker.com/r/proemergotech/nginx-rtmp-opentracing/)
[![Docker Pulls](https://img.shields.io/docker/pulls/proemergotech/nginx-rtmp-opentracing.svg)](https://hub.docker.com/r/proemergotech/nginx-rtmp-opentracing/)
[![Build Status](https://travis-ci.org/proemergotech/nginx-rtmp-opentracing.svg?branch=master)](https://hub.docker.com/r/proemergotech/nginx-rtmp-opentracing)

## Usage

For GPU support in docker check this tutorial: https://devblogs.nvidia.com/gpu-containers-runtime/

### Server
* Pull docker image and run:
```
docker pull proemergotech/nginx-rtmp-opentracing
docker run --runtime=nvidia -it -p 1935:1935 -p 8080:80 --rm proemergotech/nginx-rtmp-opentracing
```
or 

* Build and run container from source:
```
docker build -t nginx-rtmp-opentracing .
docker run --runtime=nvidia -it -p 1935:1935 -p 8080:80 --rm nginx-rtmp-opentracing
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
ffmpeg version 4.1 Copyright (c) 2000-2018 the FFmpeg developers
  built with gcc 5.4.0 (Ubuntu 5.4.0-6ubuntu1~16.04.10) 20160609
  configuration: --enable-version3 --enable-gpl --enable-nonfree --enable-small --enable-libmp3lame --enable-libx264 --enable-libx265 --enable-libvpx --enable-libtheora --enable-libvorbis --enable-libopus --enable-libfdk-aac --enable-libass --enable-libwebp --enable-librtmp --enable-postproc --enable-avresample --enable-libfreetype --enable-gnutls --enable-avfilter --enable-libxvid --enable-libv4l2 --enable-pic --enable-shared --enable-pthreads --enable-shared --enable-nvenc --enable-cuda --enable-cuvid --enable-libnpp --disable-stripping --disable-static --disable-debug --extra-cflags=-I/usr/local/cuda/include --extra-ldflags=-L/usr/local/cuda/lib64
  libavutil      55. 78.100 / 55. 78.100
  libavcodec     57.107.100 / 57.107.100
  libavformat    57. 83.100 / 57. 83.100
  libavdevice    57. 10.100 / 57. 10.100
  libavfilter     6.107.100 /  6.107.100
  libavresample   3.  7.  0 /  3.  7.  0
  libswscale      4.  8.100 /  4.  8.100
  libswresample   2.  9.100 /  2.  9.100
  libpostproc    54.  7.100 / 54.  7.100

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
    --enable-gnutls
    --enable-avfilter
    --enable-libxvid
    --enable-libv4l2
    --enable-pic
    --enable-shared
    --enable-pthreads
    --enable-shared
    --enable-nvenc
    --enable-cuda
    --enable-cuvid
    --enable-libnpp
    --disable-stripping
    --disable-static
    --disable-debug
    --extra-cflags=-I/usr/local/cuda/include
    --extra-ldflags=-L/usr/local/cuda/lib64
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
