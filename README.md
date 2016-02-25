# 目录

1. JAVA相关
2. Jfinal相关
3. Bootstrap

## 1. JAVA相关
### 1.1 从后向前取字符串

使用org.apache.commons.lang3.StringUtils库实现

``` JAVA
System.out.println(StringUtils.substringAfterLast("java1.thrift.service.address", "."));
```

输出结果：
```
address
```

### 1.2 org.apache.commons.lang3.StringUtils应用（在jpg文件扩展名前的最后加上字符‘160’）
    String imgUrl = "safdsa3290sfaf.fdaouiofdsa.jk=eq.jpg";
    String outString = StringUtils.substringBeforeLast(imgUrl, ".") + "160." + StringUtils.substringAfterLast(imgUrl, ".");
	System.out.println(outString);

输出结果：
```
safdsa3290sfaf.fdaouiofdsa.jk=eq160.jpg
```

### 1.3 字符占位替换：
```
String username="admin";
String Sql = MessageFormat.format("from user where name like ''%{0}%''", username);
```

输出结果：
```
from user where name like '%admin%'
```

另外一种实现方式（https://spring.io/guides/gs/actuator-service/）：
```
@Controller
@RequestMapping("/hello-world")
public class HelloWorldController {
    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();
    @RequestMapping(method=RequestMethod.GET)
    public @ResponseBody Greeting sayHello(@RequestParam(value="name", required=false, defaultValue="Stranger") String name) {
        return new Greeting(counter.incrementAndGet(), String.format(template, name));
    }
}
```
