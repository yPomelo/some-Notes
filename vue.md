# 第一个vue程序

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id = "app">

    {{message}}
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        data:{
            message:"hello,vue!"
        }
    });
</script>
</body>
</html>
```

导入vue对象，new一个vue，绑定一个元素，放入数据，从模板中取出来

# v-bind

v-bind:message 在标签内绑定一个值  有点像{{message}}

```html
<div id = "app">
    <span v-bind:title="message"> 鼠标悬浮会有字吗 </span>
    {{message}}
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        data:{
            message:"hello,vue!"
        }
    });
</script>
```

# v-if

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <h1 v-if="ok">yes</h1>
    <h1 v-else>no</h1>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
<script>
    var vm = new Vue({
        el:"#app",
        data:{
            ok:true
        }
    });
</script>
</body>
</html>
```

如果在浏览器控制台输入 vm.ok = false 则网页显示no

# v-for

`v-for` 指令可以绑定数组的数据来渲染一个项目列表

```html
<div id="app-4">
    <ol>
        <li v-for="todo in todos">
            {{ todo.text }}
        </li>
    </ol>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
<script>
    var app4 = new Vue({
        el: '#app-4',
        data: {
            todos: [
                { text: '学习 JavaScript' },
                { text: '学习 Vue' },
                { text: '整个牛项目' }
            ]
        }
    })
</script>
```

<img src="C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210323205101885.png" alt="image-20210323205101885" style="zoom:50%;" />

在浏览器控制台输入app4.todos.push({text:"yyy"})  会增加  4.yyy

# v-on

v-on = @

为了让用户和你的应用进行交互，我们可以用 `v-on` 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法

方法必须定义在Vue对象的methods对象中

```html
<div id="app-5">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">反转消息</button>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
<script>
    var app5 = new Vue({
        el: '#app-5',
        data: {
            message: 'Hello Vue.js!'
        },
        methods: {
            reverseMessage: function () {
                this.message = this.message.split('').reverse().join('')
            }
        }
    })
</script>
```

![image-20210323210532044](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210323210532044.png)![image-20210323210540483](C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210323210540483.png)

# v-model

`v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定

```html
<div id="app-6">
    <p>{{ message }}</p>
    <input v-model="message">
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>

<script>
    var app6 = new Vue({
        el: '#app-6',
        data: {
            message: 'Hello Vue!'
        }
    })
</script>
```

<img src="C:\Users\yyy\AppData\Roaming\Typora\typora-user-images\image-20210323213446663.png" alt="image-20210323213446663" style="zoom:50%;" />

# vue组件

```html
<div id="app-7">
    <ol>
        <!--
          现在我们为每个 todo-item 提供 todo 对象
          todo 对象是变量，即其内容可以是动态的。
          我们也需要为每个组件提供一个“key”，稍后再
          作详细解释。
        -->
        <todo-item
                v-for="item in groceryList"
                v-bind:todo="item"
                v-bind:key="item.id"
        ></todo-item>
    </ol>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
<script>
    // 定义名为 todo-item 的新组件
    Vue.component('todo-item', {
        props: ['todo'],
        template: '<li>{{ todo.text }}</li>'
    })

    var app7 = new Vue({
        el: '#app-7',
        data: {
            groceryList: [
                { id: 0, text: '蔬菜' },
                { id: 1, text: '奶酪' },
                { id: 2, text: '随便其它什么人吃的东西' }
            ]
        }
    })
</script>
```

groceryList先被遍历到item中，然后被赋值给todo作为参数传给组件的props，通过模板所以在网页上显示出来



这里看到有data属性，在vue的异步应用中还经常使用data()方法，类似于mounted()方法，data()方法的值可以绑定到其他元素上使用，第一次看的时候没看懂，这里记录一下

axios得到data放入response中，把response.data 赋值给vue对象data()里的info，就可以绑定在其他元素上使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id = "vue">
    <div>{{info.name}}</div>
    <div>{{info.address.street}}</div>

</div>

<script type="text/javascript" src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.js"></script>
<script type="text/javascript" src="https://cdn.bootcss.com/axios/0.19.0-beta.1/axios.js"></script>
<script>
    var vm =  new Vue({
        el: '#vue',
        data(){
            return{
                //请求返回的参数必须和json字符串一样
                info:{
                    name:null,
                    address:{
                        street:null,
                        city:null,
                        country:null
                    },
                }
            }
        },
        mounted(){//钩子函数 链式编程
            axios.get('data.json').then(response=>(this.info = response.data));
        }
    })
</script>
</body>
</html>
```

computed 计算属性 与methods类似，里面也是写方法的

computed内的方法通过属性来调（就是不加括号）

