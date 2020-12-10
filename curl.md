````shell
-- POST请求
curl -XPOST -d'{"m":"queryById","id":"6"}' http://127.0.0.1/api/dic

-- POST请求，添加Header
curl -H 'X-Auth-Options:1e7904f32c4fcfd59b8a524d1bad1d8a.qg0J9zG*FIkBk^vo' -XPOST -d'{"m":"login", "userName":"1000002018", "userPassword":"123456", "address":"users"}'  http://api.edu-pad.com.cn/users

-- GET请求，添加Header
curl -H 'X-Auth-Options:1e7904f32c4fcfd59b8a524d1bad1d8a.qg0J9zG*FIkBk^vo' http://api.edu-pad.com.cn/test_db
````
