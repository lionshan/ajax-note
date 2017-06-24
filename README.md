# Ajax

### Ajax XHR(原生)
1.创建对象
```js
var xml=new XMLHtpRequest()
```
2.请求

GET
```js
xml.open("请求方式(GET/POST)","地址","是否异步(true/false)")
xml.send()
```
POST
```js
xml.open("POST"," https://cnodejs.org/api/v1/accesstoken",true);
xml.setRequestHeader("Content-type","application/json");
let data={
    accesstoken:'3f77acb1-d753-4393-b784-44913190e6a8'
}
xml.send(JSON.stringify(data));

```
POST请求时：setRequestHeader(header,value)	向请求添加 HTTP 头。

header: 规定头的名称
value: 规定头的值

3.响应

获得服务器的响应，可使用XHR的属性：responseText(返回json格式)，responseXML(返回XML格式)

4.拿到后台数据

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。
当 readyState 等于 4 且状态为 200 时，表示响应已就绪.
```js
xml.onreadystatechange=function(){
    if(xml.readyState==4 && xml.status==200){
        console.log(xml.responseText)
        拿到数据为JSON格式，需要转换格式
        let data=JSON.parse(xml.responseText)
    }
}
```
XHR三个属性：
- onreadystatechange

    存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。
- readyState

    存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。

    0: 请求未初始化(打印readyState时没有0)

    1: 服务器连接已建立

    2: 请求已接收

    3: 请求处理中

    4: 请求已完成，且响应已就绪
- status

    200: "OK"

    404: 未找到页面
---
### jquery.ajax()

[查看官方文档](http://api.jquery.com/jQuery.ajax/)
GET

```js
$.ajax({
    // type:'GET'
    url:' https://cnodejs.org/api/v1/topics',
    //成功后的行为
    success:function(data){
        console.log(data)
    }
})
```
 POST请求
 ```js
$.ajax({
    type:'POST',
    dataType:'json',
    contentType:'application/json', //发往后台的数据类型
    url:' https://cnodejs.org/api/v1/accesstoken',
    data:JSON.stringify({accesstoken:'3f77acb1-d753-4393-b784-44913190e6a8'})
    }).done(function(data){
        console.log(data)
    }).fail(function(err){
        console.log(err)
    }).always(function(){
        console.log('ajax')
    })
```

解决跨域请求问题：jsonp

跨域指的是不同源(协议＋域名＋端口 有一个不同时)
```js
dataType:'jsonp',
jsonp:'callback'
```
---
### Axios

[axios](https://github.com/mzabriskie/axios)是一个基于promise的HTTP库，可以用在浏览器和node.js中。

```js  
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script> //引入axios
    axios.get('https://api.github.com/users/Jaya-lee')
    .then(res => console.log(res.data))  //后台真正的数据在res.data里
</script>
```
