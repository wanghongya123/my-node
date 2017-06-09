Express 是后端(back-and)框架，流行之一用Node.js，用来制作http　ＡＰＩ　接口的，
Express 官网是 http://www.expressjs.com.cn ,

ＵＩ和ＡＰＩ区别：UI 程序跟用户的接口，　API　是程序跟程序或者程序跟程序员的接口
Node.js 不支持import

运行nodejs 用
```js
node index.js
```

例代码
```js
const express = require("express")
const app = express()
app.listen(5000, ()=>console.log("Running on port 5000..."))
```

运行结果
```js
wanghongya@wanghongya-pc:~/Desktop/express-hello$ node index.js
Running on port 5000...
```

回调函数　格式如下：
```js
app.listen(5000, ()=>console.log("Running on port 5000..."))
```

- get 是一个http请求的**动词**接收请求
```js
app.get("/about",()=>{
  console.log("this is about page")
})
```

发请求（１）浏览器的地址栏发请求
```js
http://localhost:5000/about
```

返回字符串到页面
req 是 request 请求的简写， res 是 response 响应的简写 。res.send('Hello World'); 的作用是从后端向前端浏览器返回字符串 "this is about page"
```js
app.get("/about",(req,res)=>{
  res.send("this is about page")
})
```
###　常见错误
报错
```js
Error: listen EADDRINUSE :::5000
```
EADDRINUSE　地址已经被占用
原因：本机器另外一个服务也运行在5000端口
方法：停下服务或者修改端口号

###服务器反复重启怎么避免　nodemon

每次修改代码需要反复重启不便，安装nodemon
```js
npm install -g nodemon  
```
然后运行
```js
nodemon index.js
```

修改后就会自己不断地监听修改
```js
[nodemon] restarting due to changes...
[nodemon] starting `node index.js`
Running on port 5000...
```
