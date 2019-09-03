### Build docker

    docker-compose up --build --force-recreate

### Send data stream to server

    // On OSX (MAC)
    ffmpeg -pix_fmt uyvy422 -s 1280x720 -r 30 -f avfoundation -i "0:0" -c:v libx264 -crf 23 -preset veryfast -g 120 -keyint_min 120 -c:a aac -pix_fmt yuv420p -vf scale=640:360 -f mpegts -f flv "rtmp://localhost:1935/live/stream01"

    // Play on Raspi
    raspivid -o - -t 0 -vf -hf -fps 30 -b 6000000 | ffmpeg -re -ar 44100 -ac 2 -acodec pcm_s16le -f s16le -ac 2 -i /dev/zero -f h264 -i - -vcodec copy -acodec aac -ab 128k -g 50 -strict experimental -f flv rtmp://localhost:1935/live/stream01


### Play HLS

    // If using chrome, you need install Play HLS M3u8 extension
    http://localhost/hls/stream01.m3u8

### View Docker status

    $ docker container ls -a

### SSH to docker

    $ docker exec -it rtmp-nginx-app /bin/bash
