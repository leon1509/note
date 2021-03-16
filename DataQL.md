```
hint FRAGMENT_SQL_OPEN_PACKAGE = "off"

import 'net.hasor.dataql.fx.basic.DateTimeUdfSource' as dateTimeUtil
import 'net.hasor.dataql.fx.web.WebUdfSource' as webData;

var query = @@sql(username)<%
    set character_set_connection = 'utf8';
    select * from user where username = #{username}
%>
// return query()
// 或 输出指定列
 var userInfo = query(${username}) => [
    { "id","nickname","username", "sex", "birthday", "status" }
]
//webData.setHeader("Content-Type", "application/json; charset=UTF-8");
///
var header = webData.headerMap()
////

return userInfo => {
    "id",
    "nickname",
    "username",
    "sex": (sex == 'F') ? '男' : '女',
    "birthday": dateTimeUtil.format(birthday, 'yyyy-MM-dd'),
    "status",
    "header": header
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
