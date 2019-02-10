# Example of using ffmpeg for streaming hls with docker

## Usage 

For adding channel use this snippet in `docker-compose.yml`

```yaml
  ffmpeg_channel1:
    image: jrottenberg/ffmpeg:latest
    container_name: ffmpeg_channel1
    restart: always
    links:
      - hls_server:hls_server
    command: '-v 40
              -nostats
              -i http://example.com/channel1
              -c:a libfdk_aac -b:a 128k
              -vf yadif
              -c:v libx264 -b:v 5000k -crf 20 -profile:v main
              -s 1920x1080
              -f flv rtmp://hls_server/live/channel1'
```

## Access to streams

`http://127.0.0.1:8080/channel1.m3u8`