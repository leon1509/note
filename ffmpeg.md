### Failed to update header with correct duration |Failed to update header with correct filesize 错误如何解决
````
ffmpeg -re -i xx.mp4 -c copy -f flv -flvflags no_duration_filesize rtmp://127.0.0.1:1935/stream/

-flvflags no_duration_filesize 这个参数是关键，这个参数告诉ffmpeg不要抛出duration_filesize警告
````
