1. 在apisix中嵌入grafana

在apisix-dashboard中配置grafana地址后，需要修改grafana的配置文件 defaults.ini:
````

# 允许嵌入
allow_embedding = true
    
# 允许匿名登录
[auth.anonymous]
enabled = true
````
