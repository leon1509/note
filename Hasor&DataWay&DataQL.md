-- 1. 解决hasor4.2.3返回数据乱码
```
在application.properties中添加
server.servlet.encoding.enabled=true
server.servlet.encoding.force=true
server.servlet.encoding.charset=utf-8
或
application.yml中
server:
  servlet:
    encoding:
      enabled: true
      force: true
      charset: utf-8

```

-- 2. 示例
```
// 返回值不拆开，无论返回单条还是多条数据，都以 List/Map 形式返回
hint FRAGMENT_SQL_OPEN_PACKAGE = "off"

import 'net.hasor.dataql.fx.basic.DateTimeUdfSource' as dateTimeUtil
import 'net.hasor.dataql.fx.web.WebUdfSource' as webData;

var query = @@sql(username)<%
    select * from user where username = #{username}
%>
// return query()
// 或 输出指定列
 var userInfo = query(${username}) => [
    { "id","nickname","username", "sex", "birthday", "status" }
]
//webData.setHeader("Content-Type", "application/json; charset=UTF-8")
///
var header = webData.headerMap()
////

var sexConvert = (sex) -> {
    return (sex == 'F' ? '男' : '女');
}

return userInfo => {
    "id",
    "nickname",
    "username",
    "sex": sexConvert(sex),
    "birthday": dateTimeUtil.format(birthday, 'yyyy-MM-dd'),
    "status"//,
    //"header": header
}

==== 参数 ====

{
  "username": "Jodan"
}

==== Structure ====

{
  "success"      : "@resultStatus",
  "message"      : "@resultMessage",
  //"location"     : "@codeLocation",
  "code"         : "@resultCode",
  //"lifeCycleTime": "@timeLifeCycle",
  //"executionTime": "@timeExecution",
  "result"        : "@resultData"
}
```
--------------------

-- 3. 无需代码！通过 Dataway 配置一个带有分页查询的接口
```
https://juejin.cn/post/6844904162015068173
```

--------------------

-- 4. Dataway 整合 Swagger2，让 API 管理更顺畅
```
https://my.oschina.net/ta8210/blog/4293622
```
