---
title: ajax基本使用
tags: [ajax]
categories: [ajax]
---
# AJAX技术

异步JavaScript和xml（用js发送异步请求）

在不重新加载页面的情况下向服务器请求数据（局部刷新）

> 现今的ajax已经和xml没关系了，被json代替了



## 前后端交互的三个流程

![image-20221211141313413](/images/image-20221211141313413.png)



## 语法

~~~javascript
//(1)创建XMLHttpRequest对象
let xhr = new XMLHttpRequest()
//(2)设置请求方法和请求地址(url & method)
xhr.open('get', 'https://autumnfish.cn/api/joke')
//(3)发送请求
xhr.send()
//(4)注册响应回调事件
xhr.onload = function(){
    console.log(xhr.responseText)
}
//json转js
let res = json.parse(xhr.responseText)
~~~

get请求参数写在url后面拼接



post请求需要单独设置请求头

~~~javascript
xhr.setRequestHeader(
 'Content-type','application/x-www-form-urlencoded'
) 
xhr.send('参数名=参数')
~~~



# axios

本质是对原生 XMLHttpRequest 的封装

在服务器它使用原生node.js http模块, 而在客户端 (浏览端) 则使用XMLHttpRequest



## 语法

~~~javascript
axios
    .get('url')  
    .then(res=>{请求成功})
    .catch(res=>{请求失败})
    .then(res=>{无论是否成功})
~~~

执行post请求

~~~javascript
axios.post('url',{
    key: value
}).then(res =>{})
~~~

常用方法（传配置对象）

~~~javascript
axios({
    method: 'post',
    url: '',
    data:{post参数}, 
    params: {get参数}
}).then(res=>{}) 
~~~

data是设置请求头，把参数放在请求体里

params是把参数放在url后面拼接



## 拦截器

 在请求或响应被 then 或者 catch 处理前拦截他们

执行流程

 1. axios发送请求

 2. 执行请求拦截器

 3. 服务器处理

 4. 服务器响应

 5. 执行响应拦截器

 6. 执行axios的then方法

    

请求拦截器 

~~~javascript
axios.interceptors.request.use(
	function(config){
        return config
    },
    function(error){
        return Promise.reject(error)
    }
)
~~~

响应拦截器

~~~javascript
axios.interceptors.response.use(
	function(response){
        return response
    },
    function(error){
         return Promise.reject(error)
    }
)
~~~



## 基地址

~~~javascript
axios.defaults.baseURL = 'url'
~~~

就近原则 ：如果局部有完整的url就不访问基地址



# get和post区别

1.传参方式不同

​	get是请求行传参，随着url一并传过去

​	post是请求体传参，分为很多次传递

2.数据大小不同

​	get一般2-5mb

​	post没有大小限制

3.速度不同

​	get更快

​	post慢

4.安全性不同

​	post更安全 （ 登录、注册必须用post）



# 其他请求方式

实际开发中，按照接口文档来就行了

![image-20221213194436316](/images/image-20221213194436316.png)



# 请求报文

请求行：请求方法和请求地址

请求头：浏览器告诉服务器数据格式（图片、json等）

请求体：请求参数



# 响应报文

响应行：服务器状态码、服务器地址等

响应头：服务器告诉浏览器数据格式

响应体：服务器响应数据



# 状态码

2xx：请求成功

3xx：重定向

​	302：服务器重定向url

4xx：前端问题

​	404：url错误 	400：参数错误	 403、402：没有权限 

​	405：请求方法错误

5xx：服务器问题



# url发出到呈现的具体过程

1. DNS解析：把域名解析成ip地址
2. TCP连接 三次握手，保证HTTP网络传输是安全的
3. HTTP请求 ：浏览器发出请求、服务器处理请求、服务器响应请求
4. 浏览器渲染引擎开始渲染页面
   1. 解析html 生成dom树
   2. 解析css 生成样式树
   3. dom树和样式树合并得到渲染树
   4. 呈现页面
5. 断开连接 四次挥手



## 三次握手

- 第一次握手：客户端发送网络包，服务端收到了。
  这样服务端就能得出结论：客户端的发送能力、服务端的接收能力是正常的。
- 第二次握手：服务端发包，客户端收到了。
  这样客户端就能得出结论：服务端的接收、发送能力，客户端的接收、发送能力是正常的。不过此时服务器并不能确认客户端的接收能力是否正常。
- 第三次握手：客户端发包，服务端收到了。
  这样服务端就能得出结论：客户端的接收、发送能力正常，服务器自己的发送、接收能力也正常。

## 浏览器渲染机制

![image-20221214153802204](/images/image-20221214153802204.png)



# 文件上传

1.file表单，默认自带点击事件，作用于选择文件

2.上传文件必须使用原生内置的FormData对象

​	对象会设置单独的请求头：multipart/form-data

​	文件以二进制的方式传输

3.file表单有一个特殊的时间onchange时间，用户选择好就会执行

