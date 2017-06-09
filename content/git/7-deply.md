# VUE.js   https://cn.vuejs.org

用data渲染hellow VUE
```html
<body>
  <div id="app">
    {{ msg }}
  </div>
  <script src="./vue.js"></script>
  <script>
    var vm = new Vue({
      el:"#app",
      data:{
        msg:"hello vue"
      }
    })
  </script>
</body>
```
el:"#app" 挂载到app上 和　new Vue({}).$mount("#app")　功能一样
单独输出el就是 输出结果是【  <div id="app">
    我的消息是：hello vue
  ８
  </div>】
```js
console.log(vm.$el)
```

字符串拼接的方法用{{}}
```js
  {{` 我的消息是：${msg} ${msg.slice(5)} `}}
```
定义多个data
```js
var vm = new Vue({
    el:"#app",
    data:{
      msg:"hello vue",
      num: 8
    }
  })
```
###指令　　“v-xx” 例如v-text
指令写法等同于{{num}}，输出的结果都是８
```js
  <p>{{num}}</p> //8
  <p v-text="num+2"></p> //10
```
v-html 把插入的dom块渲染出来
```js
var vm = new Vue({
    el:"#app",
    data:{
      num1:"<span>hahha</span>"
    }
  })
```
```js
  <p v-html="num1"></p> //hahha
```
v-cloak 属性标签,隐藏用大括号写的标签中的双大括号
```js
<style>
  [v-cloak]{
    display: none;
  }
</style>
```
```js
<div id="app" v-clock>
    {{` 我的消息是：${msg} ${msg.slice(5)} `}}
    {{num}}
```
v-once  只渲染一次
不加　v-once 在３秒后“hello vue”变成“你好”,加上之后不变
```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <div id="app" v-cloak v-once>
    {{` 我的消息是：${msg} ${msg.slice(5)} `}}
  </div>
  <script src="./vue.js"></script>
  <script>
    var vm = new Vue({
      el:"#app",
      data:{
        msg:"hello vue",
      }
    })
    setTimeout(function(){
      vm.msg="你好"
    },3000)
    console.log(vm.$el)
  </script>
</body>
</html>
```
v-if 条件渲染　v-else v-if v-else-if 条件 是不是插入
```js
data:{
  show:false
}
```
```js
<div v-if="show">hahah</div>  //在页面没有这个div
```
template  拯救被破坏的队形
v-show 显示不显示判断用 加了一个display:none;
```js
<h1 v-show="ok">Hello!</h1>
```
v-for相当于map　遍历数组 在li中写"v-for="item in todos""就遍历了数组　
```html
<div id="app">
   <ul>
     <li v-for="(item,i ) in todos" >
       index:{{i}}--{{item.id}}--{{item.text}}
     </li>
   </ul>
</div>
  <script src="./vue.js"></script>
  <script>
    var vm = new Vue({
      el:"#app",
      data:{
       todos:[
         {id: 1 ,text: "do what"},
         {id: 2 ,text: "do what2"},
         {id: 3 ,text: "do what3"},
         {id: 4 ,text: "do what4"}
       ]
      }
    })
  </script>
```
v-for 对象遍历
```html
<div v-for="(item,key,index) in obj">
      <h3>{{key}}:{{item}}:{{index}}</h3>
</div>
```
```js
new Vue({
  el: '#repeat-object',
  data: {
    obj: {
      FirstName: 'John',
      LastName: 'Doe',
      Age: 30
    }
  }
})
```
v-bind  绑定元素属性 v-bind:元素属性:="属性值"
```html
<div v-bind:id="box"></div>
```
就相当于
```html
<div id="box"></div>
```
也可以用三木判断
```html
<div id="app">
    <div v-bind:id="id" :class='id?"box":"box2"'>hello</div>
  </div>
    <script src="./vue.js"></script>
  <script>
    var vm = new Vue({
      el:"#app",
      data:{
        id:"hello"
      }
    })
    vm.id = "word"
  </script>
```
v-model 表单绑定
```html
<div id="app">
  <p>{{msg}}</p>
  <input type="text" name='msg' v-model="msg">
</div>
<script src="./vue.js"></script>
<script>
var vm = new Vue({
  el:"#app",
  data:{
    msg:"hello word"
  }

})
</script>
```
单选框　v-model="checked"

多个勾选框，绑定到同一个数组： v-model="checkedNames"
```html
<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>
<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>
<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
<br>
<span>Checked names: {{ checkedNames }}</span>
```
```js
new Vue({
  el: '...',
  data: {
    checkedNames: []
  }
})
```
单选按钮　v-model="picked">
```html
<div id="example-4" class="demo">
  <input type="radio" id="one" value="One" v-model="picked">
  <label for="one">One</label>
  <br>
  <input type="radio" id="two" value="Two" v-model="picked">
  <label for="two">Two</label>
  <br>
  <span>Picked: {{ picked }}</span>
</div>
```
```js
new Vue({
  el: '#example-4',
  data: {
    picked: ''
  }
})
```
单选列表: v-model="selected"
```html
<div id="example-5" class="demo">
  <select v-model="selected">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>
</div>
```
```js
new Vue({
  el: '#example-5',
  data: {
    selected: null
  }
})
```
多选列表（绑定到一个数组）：v-model="selected"
```html
<div id="example-6" class="demo">
  <select v-model="selected" multiple style="width: 50px">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <br>
  <span>Selected: {{ selected }}</span>
</div>
```
```js
new Vue({
  el: '#example-6',
  data: {
    selected: []
  }
})
```
如果想自动将用户的输入值转为 Number 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个修饰符 number 给 v-model 来处理输入值 : v-model.number

如果要自动过滤用户输入的首尾空格，可以添加 trim 修饰符到 v-model 上过滤输入： v-model.trim
##　计算
```html
<div id="app">
  <table>
    <thead>
      <tr>
        <th>书名</th>
        <th>价钱</th>
        <th>数量</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in book">
        <th>{{item.name}}</th>
        <th>{{item.price}}</th>
        <th><input type="number" v-model.number="item.num"></th>
      </tr>
    </tbody>
  </table>
  <h1>总价为：{{totalMoney}} 元</h1>
</div>
```
```js
var vm = new Vue({
    el:"#app",
    data:{
      book:[
        {name:"node.js",price:5,num:3},
        {name:"react.js",price:6,num:2},
        {name:"vue.js",price:8,num:3},
        {name:"jq.js",price:1,num:6}
      ]
    },
    computed:{
      totalMoney:function(){
        let total = 0;
        this.book.forEach(item=>total+=item.price*item.num)
        return total
      }
    }

  })
</script>
```
