# 目录

1. JAVA相关
2. Jfinal相关
3. Bootstrap

## 1. JAVA相关
___
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

### 1.4 List 去重
```
private List<Language> getLanguages(List<ResPo> resources) {
	List<Language> resList = new ArrayList<Language>();
	for (ResPo resPo : resources) {
		Language lang = new Language();
		lang.setCode(resPo.getLanguageId());
		resList.add(lang);
	}
	
	Set<Language> s = new TreeSet<Language>(new Comparator<Language>() {
		public int compare(Language o1, Language o2) {
			return o1.getCode().compareTo(o2.getCode());
		}
	});
	s.addAll(resList);
	return new ArrayList<Language>(s);
}
```

## 2. Jfinal相关
___
### 2.1 IE渲染JSON
```
render(new JsonRender(data).forIE());
```

### 2.2 poi生成Excel
```
String[] headers = new String[] { "电话号码", "设备id", "imsi"};
List<Record> list = Account.dao.getStudentAccountList(class_id);
render(PoiRender.me(list).fileName("test.xls").headers(headers).cellWidth(5000).headerRow(2));
```

### 2.3 让 模版 可以使用session
configInterceptor方法中添加：
```
me.add(new SessionInViewInterceptor());
```

### 2.4 向ORACLE数据库插入带时间的日期类型数据
```
Date d = new Date(); //java.util.Date
r.set("Update_Time", new java.sql.Timestamp(d.getTime()));
```

### 2.5 过滤所有对静态资源以及jsp、html等的请求
configHandler方法中添加：
```
// 以下正则将匹配带有扩展名的文件请求，扩展名最短1位，最长4位。可根据需要灵活配置正则。
arg0.add(new UrlSkipHandler(".+\\.\\w{2,4}", false));
```

## 3. Bootstrap
___
### 3.1 bootstrap-select插件清除选择，一般用于FORM表单的重置
```
$("#qSys").selectpicker('deselectAll');
```
### 3.2 choosen
```
隐藏搜索的单选功能：$(".chosen-select").chosen({disable_search_threshold: 10});
设置多选的最大选择数：$(".chosen-select").chosen({max_selected_options: 5});
监听更新事件：$("#form_field").chosen().change( … );
手动触发更新：$("#form_field").trigger("chosen:updated");
自定义宽度：$(".chosen-select").chosen({width: "95%"});
指定选择值：$('#q_continentID option:first').attr('selected','selected');	// 指定选项值到第一项
```
### 3.3 一行显示label和input（在label的style中加入display:inline）
```
<form class="bs-docs-example" style="padding-bottom: 15px;">
	<div class="controls">
		<label class="control-label" for="inputEmail" style="display:inline;">Email</label>
		<input class="span5" type="text" placeholder=".span5">
	</div>
	<div class="controls controls-row">
		<input class="span4" type="text" placeholder=".span4">
		<input class="span1" type="text" placeholder=".span1">
	</div>
</form>
```
### 3.4 用tab显示ajax内容
第一步定义面板，代码如下：
```
	<!-- TAB面板 -->
	<ul  class="nav nav-tabs" id="homeKeyTab">
            <li class="active"><a href="#home" data-toggle="tab">首页</a></li>
            <li><a href="#profile" data-toggle="tab">介绍</a></li>
            <li><a href="#messages" data-toggle="tab">消息</a></li>
            <li><a href="#settings" data-toggle="tab">设置</a></li>
        </ul>
        <div class="tab-content">
            <div class="tab-pane fade in active" id="home"></div>
            <div class="tab-pane fade" id="profile"></div>
            <div class="tab-pane fade" id="messages"></div>
            <div class="tab-pane fade" id="settings"></div>
        </div>
```
第二步写JS，如下：
```
	$(function(){
		// tab点击触发事件
		$('#homeKeyTab a').click(function (e) { 
			e.preventDefault();//阻止a链接的跳转行为 
			$(this).tab('show');//显示当前选中的链接及关联的content 
		});
		// 显示第一个面板的内容
		//load content for first tab and initialize
		$('.tab-content div:first').load(uri.contents, function() {
			$('#homeKeyTab').tab(); //initialize tabs
		});
		// 切换面板时更新面板的内容
		$('#homeKeyTab').bind('show', function(e) {
			var pattern=/#.+/gi //use regex to get anchor(==selector)
			var contentID = e.target.toString().match(pattern)[0]; //get anchor         
			//load content for selected tab
			$(contentID).load(uri.contents + contentID.replace('#',''), function(){
				$('#homeKeyTab').tab(); //reinitialize tabs
			});
		});
	});
```
### 3.5 文件上传无刷新（http://blog.csdn.net/cl05300629/article/details/11151547）
把form的target设为页面里一个看不见的iframe，这样上传时候就不会刷新页面了，比如 ：
```
<form action="uploadFile" method="post" enctype="multipart/form-data" target="upload">  
<input id="uploadfile" name="uploadfile" type="file"/><button>上传至FTP</button>  
</form>
<iframe name="upload" style="display:none"></iframe> 
```
