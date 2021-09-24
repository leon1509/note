-- 在当前目录、8888端口启动http服务
````
$ nohup python3 -m http.server 8888 &
````

-- 关闭phthon启动的http服务
````
$ netstat -nutap | grep python3
````
tcp            0      0 0.0.0.0:8888                  0.0.0.0:*    LISTEN          49668/python3
````
$ kill -9 49668
````
