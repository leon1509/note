# 代理第三方接口
在nginx.conf中，添加以下配置：

'''
location /gatewayproxy/ {    -- 注意最后面的/
    proxy_pass https://gatewayproxy-jcpt.mwr.cn/;    -- 注意最后面的/

    proxy_http_version 1.1;
    proxy_set_header Connection "";
    proxy_redirect off;   -- 注意
    rewrite ^/gatewayproxy/(.*)$ /$1 break;  -- 注意
}
'''
经上面的代理后，
原接口地址：https://gatewayproxy-jcpt.mwr.cn/riverdetails/getElementDetailNoEncrypt?k=xxxxxxxxxxxxxxxxxxxxx 将代理为：https://tgp.mwr.cn/gatewayproxy/riverdetails/getElementDetailNoEncrypt?k=xxxxxxxxxxxxxxxxxx

原接口地址：https://gatewayproxy-jcpt.mwr.cn/rswbdetail/getElementDetailNoEncrypt?k=xxxxxxxxxxxxxxxxxxxxx 将代理为：https://tgp.mwr.cn/gatewayproxy/rswbdetail/getElementDetailNoEncrypt?k=xxxxxxxxxxxxxxxxxx

原接口地址：https://gatewayproxy-jcpt.mwr.cn/riverlist/river?k=xxxxxxxxxxxxxxxxxxxxx 将代理为：https://tgp.mwr.cn/gatewayproxy/riverlist/river?k=xxxxxxxxxxxxxxxxxx
