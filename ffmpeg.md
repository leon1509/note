### 流媒体服务器
````
https://github.com/aler9/rtsp-simple-server

支持以rtsp（默认端口8854）和rtmp（默认端口1935）推流：
    - rtsp://10.1.4.144:8554/stream
    - rtmp://10.1.4.144:1935/mystream

以rtsp和rtmp形式发布流后，都可以用HLS方式访问（默认端口是8888）：http://10.1.4.144:8888/mystream

支持windows、linux、macOS

````

### Failed to update header with correct duration |Failed to update header with correct filesize 错误如何解决
````
ffmpeg -re -i xx.mp4 -c copy -f flv -flvflags no_duration_filesize rtmp://127.0.0.1:1935/stream/

-flvflags no_duration_filesize 这个参数是关键，这个参数告诉ffmpeg不要抛出duration_filesize警告
````
### ffmpeg推流(可解决上面的问题）
````
**** 此条语句可解决上面的问题****
ffmpeg -re -i 我的真朋友\ 02.mp4 -vcodec libx264 -vprofile baseline -acodec aac -ar 44100 -strict -2 -ac 1 -f flv -s 1280x720 -q 10 rtmp://127.0.0.1:1935/stream/

基本语法：ffmpeg -re -i a.mp4 -c:a copy -c:v copy -f flv rtmp://127.0.0.1:1935/live/
-re表示按文件中音视频流的码率推送，如果不加，就是不控制发送速度，一次性发送给服务端了，不符合直播的特点
-stream_loop -1表示文件结束后，继续从文件头部循环推送的次数，-1表示无限循环
-i表示输入文件
-c:a copy表示音频编码格式不变
-c:v copy表示视频编码格式不变
-f flv推送rtmp流需要指定格式为flv
最后是rtmp推流地址
如果是mp4文件，将demo.flv换成mp4文件名即可，比如demo.mp4


其它推流方式：cat example.mp4 | ffmpeg -re -i pipe:0 -c:v copy -c:a copy -f flv rtmp://127.0.0.1:1935/live/
````

### RTSP和RTMP推流（示例）
````
推rtsp： ffmpeg -re -stream_loop -1 -i 1.mp4 -c copy -f rtsp rtsp://10.1.4.144:8554/stream
推rtmp： ffmpeg -re -stream_loop -1 -i 1.mp4 -vcodec copy -acodec copy -f flv rtmp://127.0.0.1:1935/stream/

````

### 视频压缩
````
视频压缩方法1： ffmpeg -i 彩妆.mp4 -vcodec libx264 -crf 24 cz1.mp4  -- 比特率自动随编码器
视频压缩方法2： ffmpeg -i 彩妆.mp4 -b 2000K cz.mp4   -- 指定比特率
````

### 视频截取： 
````
ffmpeg -ss 00:02:14 -i 30.mkv -vcodec copy -acodec copy 30.mp4
ffmpeg -ss 00:00:00 -t 00:00:30 -i test.mp4 -vcodec copy -acodec copy output.mp4
* -ss 指定从什么时间开始
* -t 指定需要截取多长时间
* -i 指定输入文件
````

### 字幕 软订阅
````
在文件中作为单独流包含的字幕。播放器可以打开/关闭它们，并且不需要重新编码视频流。

ffmpeg -i input.mkv -c copy -c:s mov_text output.mp4    播放器对MP4中的定时文本软字幕的支持可能会很差。您只需要尝试一下。
````

### 字幕 硬订阅
````
硬字幕被“刻录”到视频中，因此必须对视频进行重新编码。

ffmpeg -i input.mkv -vf subtitles=input.mkv output.mp4

ffmpeg -i 02.mkv -vf subtitles=02.mkv -vcodec libx264 -crf 24 002.mp4
````
