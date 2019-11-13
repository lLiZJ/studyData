```java
@RequestMapping(value="/test", method = RequestMethod.POST, produces = {"application/json;charset=UTF-8"})
	@ResponseBody
	public String test1(@RequestParam(value = "name", required = false) String name, @RequestBody Student stu) {
		System.out.println("你来啦");
		stu.setName(name);
		System.out.println(stu.getStuid());
		System.out.println(stu.getName());
		System.out.println(stu.getSex());
		if(studentService.addStudent(stu)) {
			System.out.println("添加成功");
			return "添加成功";
		}else {
			return "添加失败";
		}
	}
```
## @ResponseBody
* @ResponseBody是作用在方法上的，@ResponseBody 表示该方法的返回结果直接写入 HTTP response body 中，一般在异步获取数据时使用【也就是AJAX】
* 在使用 @RequestMapping后，返回值通常解析为跳转路径，但是加上 @ResponseBody 后返回结果不会被解析为跳转路径，而是直接写入 HTTP response body 中。 比如异步获取 json 数据，加上 @ResponseBody 后，会直接返回 json 数据
## @RequestBody
* @RequestBody 将 HTTP 请求正文插入方法中，使用适合的 HttpMessageConverter 将请求体写入某个对象（**例如上面的Student**）
* @RequestBody是作用在形参列表上，用于将前台发送过来固定格式的数据【xml 格式或者 json等】封装为对应的 JavaBean 对象（**例如上面的Student**），封装时使用到的一个对象是系统默认配置的 HttpMessageConverter进行解析，然后封装到形参上
## @RequestParam
* @RequestParam是传递参数的
* @RequestParam用于将请求参数区数据（**url后面跟着的或form格式提交的**）映射到功能处理方法的参数上。
* @RequestParam注解主要有哪些参数：
    * value：参数名字，即入参的请求参数名字，如username表示请求的参数区中的名字为username的参数的值将传入
    * required：是否必须，默认是true，表示请求中一定要有相应的参数，否则将报404错误码
    * defaultValue：默认值，表示如果请求中没有同名参数时的默认值，默认值可以是SpEL表达式，如“#{systemProperties['java.vm.version']}”
* 但是在传递参数的时候如果是 **url?userName=zhangsan&userName=wangwu** 时怎么办呢?其实在实际roleList参数入参的数据为“zhangsan,wangwu”，即多个数据之间使用“，”分割；我们应该使用如下方式来接收多个请求参数：
    * `public String requestparam8(@RequestParam(value="userName") String []  userNames)`
    * `public String requestparam8(@RequestParam(value="list") List<String> list)`
## @RequestParam和@RequestBody这两个注解是可以同时使用的

