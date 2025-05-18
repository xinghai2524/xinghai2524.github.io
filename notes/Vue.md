# 目录

[TOC]

# 第二章

## **v-once**

用于制定元素或者组件只渲染一次

## **v-text**

相当于插值语法，用于更新元素的textContent

## **v-pre**

用于跳过元素及其子元素的编译过程，也就是不去计算变量和函数，而是直接当成字符串输出

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app"></div>
    <template id="www">
        <div v-pre >{{ message }}</div>
        <div v-pre >{{ print(a) }}</div>
        <div>{{ message }}</div>
        <div>{{ print("asdfasdf") }}</div>
    </template>
    <script src="../js/vue.js" ></script>
    <script>
        Vue.createApp({
            template:'#www',
            data:()=>{
                return {
                    message:'abc'
                }
            },
            methods:{
                print(a){
                    return a
                }
            }
        }).mount('#app')
    </script>
</body>
</html>
```

**效果**

![image-20241116200949103](https://db.xinghai.ink/Typora/1734987107788057.png)

## **v-cloak**

在没有模板没有编译完成之前，会显示v-cloak标签对应的css样式

## **v-bind**

用于绑定标签的属性，也就是给标签的属性赋值，具体语法如下

```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app" ></div>
    <template id="my-app" >
        <!-- 语法糖 -->
        <img :src="url">
        <!-- 语法 -->
        <img v-bind:src="url">
    </template>
    <script src="../js/vue.js" ></script>
    <script>
        Vue.createApp({
            template:'#my-app',
            data(){
                return {
                    url:'https://v2.cn.vuejs.org/images/logo.svg'
                }
            },

        }).mount('#app')
    </script>
</body>
</html>
```

**效果**

![image-20241116203952161](https://db.xinghai.ink/Typora/17349869744435828.png)

### 绑定class属性的方法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>title</title>
</head>
<body>
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <h2 :class="'app'" >class绑定字符串1</h2>
            <h2 :class="className" >绑定字符串2</h2>
            <h2 :class="{'active':isActive}" >绑定对象</h2>
            <h2 :class="{active:isActive}" >绑定对象2</h2>
            <h2 :class="{active:isActive,title:true}" >绑定对象3</h2>
            <h2 class='abc cba' :class="{active:isActive,title:true}" >绑定对象4</h2>
            <h2 class='abc cba' :class="aObject" >绑定对象5</h2>
            <h2 class='abc cba' :class="getObject()" >绑定对象6</h2>
            <button @click="toggle" >点我</button>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    className:"Hello World",
                    isActive:true,
                    aObject:{
                        'activate':false,
                        'title':true
                    }
                }
            },
            methods:{
              getObject(){
                return {
                    'activate':false,
                    'title':true   
                }
              },
              toggle(){
                this.isActive = !this.isActive
              }
            }
        }).mount('#app')
    </script>

</body>
</html>
```

- `{‘className’,boolean}`中className表示将要放入的值，而boolean布尔值决定了前面的值是否放入
- `:class='object'`中，`object`可以是字符串，可以是变量，也可以是对象，他们可以通过变量返回类、对象、字符串，也可以通过函数返回这些，比如上面的`getObject()`就是通过函数返回的对象插入到class中

**数组**

数组可以使用对象的表达式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app" ></div>
    <template id="my-app">
        <div :class="['abc',title]" >绑定数组</div>
        <div :class="['abc',title, isActivate ? 'activate':'false']" >绑定数组</div>
        <div :class="['abc',title, isActivate ? 'activate':'false',{ac:isActivate}]" >绑定数组加上对象</div>
    </template>
    <script src="../js/vue.js" ></script>
    <script>
        Vue.createApp({
            template:'#my-app',
            data(){
                return {
                    title:'title',
                    isActivate:true
                }
            },
            methods:{

            }
        }).mount('#app')
    </script>
</body>
</html>
```

- 用v-bind绑定的class支持数组、对象、变量、字符串等形式

### 绑定style属性的方法

```html
            <h2 :style="{color:finalColor,fontSize: '16px'}">a</h2>
            <h2 :style="{color:finalColor,fontSize: fontSize + 'px' }">b</h2>
```

- 这个和绑定class不同，这里面的对象的属性是一定会被渲染的，而值则是根据变量进行显示
- 第二个支持字符串拼接

**数组**

```html
    <template id="my-app" >
        <div>
            <h2 :style="[{'color':finalColor,'fontSize':'16px'}]">abc</h2>
            <h2 :style="[styleObj,styleObj2,stylefunc()]">abc</h2>
        </div>
    </template>
```

同理，数组的效果其实就是几个对象相加

### 动态绑定属性和值

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <h2 :[name]="value" >hahaha</h2>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    name:'style',
                    value:{
                        color:'red'
                    }
                }
            },
            methods:{
              
            }
        }).mount('#app')
    </script>

</body>
```

- 其实就是给属性加上了个中括号，然后就可以定义属性和值的变量了

### 绑定对象

```html
<body>
    <div id="app"></div>

    <template id="my-app">
        <div>
            <h2 :="info" >asdfasdf</h2>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    info:{
                        style:[{color:'red'},{background:'black'},{width:'100px'},{height:'100px'},{margin:'100px auto'}],
                        class:['abc','eee','asdf','asd']
                    }
                }
            },
            methods:{
              
            }
        }).mount('#app')
    </script>

</body>
```

- 在h2中使用v-bind绑定了一个五名称的值，我们往这个值传递对象，就会被直接替换成属性和值

## v-on

这个指令用于绑定事件，绑定的方式和v-bind相似，就像`:`是v-bind的语法糖，`@`是v-on的语法糖，具体操作如下

```html
<body>
    <div id="app" ></div>
    <template id="my-app" >
        <button v-on:click="btn1Click" >监听按钮，完整版</button>
        <div class="area" v-on:mouseMove="mouseMove" >监听鼠标移动事件</div>
        <button @click="btn1Click" >监听按钮，简写</button>
        <div class="area" @mouseMove="mouseMove">监听鼠标移动事件，简写</div>
        <div class="area" @mousemove="mouseMove" @click="btn1Click">点击和监听</div>
        <div class="area" @="{click:btn1Click,mousemove:mouseMove}">点击和监听</div>
    </template>
    <script src="../js/vue.js" ></script>
    <script>
        Vue.createApp({
            template:'#my-app',
            data(){return{
                message:'hellow Word',
                counter:100
                }},
            methods:{
                btn1Click(){
                    console.log('点击了一下')
                },
                mouseMove(){
                    console.log('移动了一下')
                }
            },
        }).mount('#app')
    </script>
</body>
```

- 事件绑定是不支持数组的

### 事件对象和传递参数

事件发生时会产生事件对象，我们可以在回调函数中获取事件对象

在javascript会自动传入对象的，在方法中的第一个参数就是事件对象

```html
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <h2 @click="print" :="info" >eeee</h2>
            <!-- 显式调用 -->
            <h2 @click="print($event)" :="info" >eeee</h2>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    info:{
                        style:{color:'red',width:'100px',height:'100px',background:'#ddd'}
                    }
                }
            },
            methods:{
              print(ee){
                console.dir(ee.target)
              }
            }
        }).mount('#app')
    </script>
```

- 其中，可以使用$event用来显式的传入参数，当然默认情况下也会自动传入

### 修饰符

事件冒泡：指的是在一个控件中被点击，他的点击事件会不断传入上一级目录，例如，div标签包含p标签，两个标签都有点击事件监听，则如果点击p标签，那么两个标签都会触发事件，这是由于p标签也是div的一部分

在一些特定的场景下，我们不需要事件继续往上冒泡，则需要阻止冒泡，在vue中，可以使用修饰符阻止事件冒泡

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <div @click="divClick" :style="{width:'100px',height:'100px',background:'#ddd'}">
                <button @click.stop="btnClick" >阻止冒泡</button>
                <button @click="btnClick" >不阻止冒泡</button>
            </div>
            <input type="text" @keyup.enter="enterKeyup" >
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    message:"Hello World"
                }
            },
            methods:{
              divClick(){
                console.log('divClick')
              },
              btnClick(){
                console.log('btnClick')
              },
              enterKeyup(e){
                console.dir(e.target)
              }
            }
        }).mount('#app')
    </script>

</body>
```

- 在示例代码中出现一个新的修饰符是keyup，keyup是键盘抬起的修饰符，每敲击一次键盘就触发一次函数，如果想在用户输入完成后敲击enter键再触发函数，则再后面添加enter修饰符

## 条件渲染

在前端开发中，有时需要根据当前条件决定是否渲染特定的元素或者组件

### v-if

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <h2 v-if="isShow" >条件渲染</h2>
            <button @click="toggle" >切换</button>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    isShow:true
                }
            },
            methods:{
              toggle(){
                this.isShow = !this.isShow
              }
            }
        }).mount('#app')
    </script>

</body>
```

- 只有v-if为true的时候才会被渲染

### v-if,v-else,v-else-if

这三个指令其实对应的是JavaScript的if else 和 else if 语句

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <input type="text" v-model="score" >
            <div v-if="score >= 90" >优秀</div>
            <div v-else-if="score >= 60" >及格</div>
            <div v-else>不及格</div>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    score:'',
                    s:''
                }
            },
            methods:{
              
            }
        }).mount('#app')
    </script>

</body>
```

当然，可以嵌套使用

```html
<div>
    <input type="text" v-model="score" >
    <input type="text" v-model="s" >
    <div v-if="score >= 90" >
        优秀
        <br/>
        <div v-if="s >= 90" >非常优秀</div>
        <div v-else>还行</div>
    </div>
    <div v-else-if="score >= 60" >及格</div>
    <div v-else>不及格</div>
</div>
```

### v-if和template结合使用

在开发中，可能会需要一次性隐藏很多个标签，然而，如果在某个标签上面使用v-if，然后在这个标签下添加多个div标签也能实现效果，但是实际上他还是控制单个标签的隐藏，如果想要隐藏多个标签，则可以使用template标签作为多个标签的父标签，再控制父标签，使用template，并不会显示这个标签，而是直接将多个标签显示出来，从而去除了父标签

![image-20241117214056613](https://db.xinghai.ink/Typora/17349869888366692.png)

### v-show

```html
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <h2 v-show="isShow">
                isShow 条件渲染基本使用
            </h2>
            <button @click="toggle">按钮</button>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    isShow:true
                }
            },
            methods:{
                toggle(){
                    this.isShow = !this.isShow
                }
            }
        }).mount('#app')
    </script>
```

**v-show和v-if的区别在于**

- v-show不支持在template中使用
- v-show不能和v-if一起使用
- v-show无论是否被渲染都会被显示在DOM上，本质上是通过display控制的
- 当v-if的条件为false时，对应的元素不会被渲染到DOM树上

## 列表渲染

### v-for

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <ul>
        <li v-for="movie in movies" >{{ movie }}</li>
        </ul>
        <ul>
        <li v-for="(movie,index) in movies" >{{ index + 1 }}-{{ movie }}</li>
        </ul>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    movies:[
                        '新机穿越',
                        '盗梦空间',
                        '少年派',
                        'abc'
                    ]
                }
            },
            methods:{
              
            }
        }).mount('#app')
    </script>

</body>
```

v-for支持许多类型

- 遍历值：v-for="value in Object"
- 遍历键值对：v-for="(value,key) in object"
- 遍历键值对：v-for="(value,key,index) in object"
- 遍历数字：v-for="(value,index) in Nunber"

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <h2>遍历对象</h2>
            <ul>
                <li v-for="(v,k,i) in info" >{{ i }}--{{ v }},{{ k }}</li>
            </ul>
            <h2>遍历数字</h2>
            <ul>
                <li v-for="(v,i) in 99" >{{v}},{{ i }}</li>
            </ul>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    info:{
                        name:'xinghai',
                        age:18,
                        height:1.76
                    }
                }
            },
            methods:{
              
            }
        }).mount('#app')
    </script>

</body>
```

### v-for和template

同样，使用template标签的用处就是循环之后不会显示template标签，而是直接显示子标签

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <ul>
            <template v-for="(v,k) in info" >
                <li>{{ k }}</li>
                <li>{{ v }}</li>
                <li :style="{height:'2px',background:'#ddd'}" ></li>
            </template>
        </ul>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    info:{
                        name:'xinghai',
                        age:18,
                        height:1.76
                    }
                }
            },
            methods:{
              
            }
        }).mount('#app')
    </script>

</body>
```

效果

![image-20241117235140966](https://db.xinghai.ink/Typora/17349869978794165.png)

### 数组的更新检测

在遍历数组或使用数组渲染时，与变量一样，只要改变了值，都会被实时渲染在页面上

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <ul>
            <li v-for="(v,index) in message" >{{v}}     <button @click="quchu(index)">-</button></li>
        </ul>
        <input type="text" v-model="value" >
        <br>
        <button @click="add_push" >添加</button>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    message:[
                        'asdff',
                        'eqe',
                        '7hh',
                        'pl'
                    ],
                    value:''
                }
            },
            methods:{
              add_push(){
                this.message.push(this.value)
                this.value = ''
                console.log(this.message)
              },
              quchu(index){
                this.message.splice(index,1)
                console.log(this.message)
              }
            }
        }).mount('#app')
    </script>

</body>
```

- 有一点需要注意，一个模板相当于一个函数，然后每个函数都有其对应的命名空间，比如，v-for如果定义了value和index两个属性，那么在其子函数或者说子标签中都可以直接使用value和index变量，这个变量的使用方法和data函数类似

## key和diff算法

在使用v-for时，官方推荐为元素绑定一个key属性，这样做是为了更好的执行diff算法，斌确定需要怎删改查的元素位置，需要注意的是，一定要保证key的唯一性

# 第三章

## 计算属性

模板中，可以通过插值语法显示一些data属性中的数据，但是在某些场景下需要将数据处理后再进行显示，例如，需要对数据进行运算或者由三元运算符决定结果，因此可以使用两种方法

- 将逻辑抽取到一个方法中，也就是放在methods选项中
- 使用计算属性(computed)

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <div>
            <h2>{{ getFullName() }},{{a}}</h2>
            <h2>{{ getFullName() }},{{a}}</h2>
            <h2>{{ getFullName() }},{{a}}</h2>
            <h2>{{ getFullName() }},{{a}}</h2>

            <h2>{{ FullName }},{{a}}</h2>
            <h2>{{ FullName }},{{a}}</h2>
            <h2>{{ FullName }},{{a}}</h2>
            <h2>{{ FullName }},{{a}}</h2>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    firstName:'kobe',
                    lastName:'Bryant',
                    a:''
                }
            },
            methods:{
              getFullName(){
                console.log('调用了methods')
                return this.firstName + " " + this.lastName
              }
            },
            computed:{
                FullName(){
                console.log('调用了FullName')
                return this.firstName + " " + this.lastName
              }
            }
        }).mount('#app')
    </script>

</body>
```

关于methods和compute：

- methods是没有办法保存缓存的，每次调用函数都是执行一次
- computed调用函数之前会看有没有缓存，如果是重复调用，则会返回上一次的结果，如果是依赖属性出现了修改才会重新执行一次

​	在computed中，可以定义属性，而属性可以包含get函数和set函数，get函数会在模板调用属性时运行，set函数会在赋值是运行，赋值会被当成set函数的参数传入

```html
<body>
    <div id="app"></div>

    <template id="my-app" >
        <button @click="changeFullName" >修改 fullName</button>
        <h4>{{ fullName }}</h4>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    firstName:'kobe',
                    lastName:'Bryant'
                }
            },
            methods:{
              changeFullName(){
                this.fullName = "Coder why";
              }
            },
            computed:{
                fullName:{
                    get:function(){
                        return this.firstName + this.lastName
                    },
                    set:function(NewValue){
                        console.log(NewValue);
                        const names = NewValue.split(' ');
                        this.firstName = names[0];
                        this.lastName = names[1];
                    }
                }
            }
        }).mount('#app')
    </script>

</body>
```

## 监听器

```html
    <script>
        Vue.createApp({
            template:'#my-app',
            data:()=>{
                return{
                    message:{name:'abc',age:18,book:{name:"vue.js"}}
                }
            },
            methods:{
              changeMessage(){
                this.message = {name:'aab',age:18,book:{name:"vue.js"}}
              },
              changeName(){
                this.message.name = 'hahaha'
              },
              changeBookName(){
                this.message.book.name = '666'
              }
            },
            watch:{
                message:{
                    handler:function(newValue,oldValue){
                        console.log(newValue,oldValue)
                    },
                    deep:true,
                    immediate:true
                }
            }
            ,
            computed:{
              
            }
        }).mount('#app')
    </script>

</body>
```

​	具体来说，watch支持监听变量，当变量出现改变时，则执行对应的函数、

- watch的语法为`变量:{haddler:function(){},deep:false,immediate:true}`

**watch高级用法**

​	watch可以是在变量里面设置handler，deep，immediate等，也可以直接传入函数名称，和函数列表，例如

```html
<div id="app"></div>

<template id="my-app">
    <h3>{{ message }}</h3>
    <button @click="changeMessage">改变message</button>
</template>

<script src="../js/vue.js"></script>

<script>
    Vue.createApp({
        template: '#my-app',
        data: () => {
            return {
                message: "Hello World",
                oldMessage : 'hahaha'
            }
        },
        methods: {
            changeMessage() {
                this.message = this.oldMessage
            },
            print(New,Old){
                console.log(New,Old)
            }
        },
        watch: {
            message:[
                    function (New,Old) { console.log('函数1');this.oldMessage = Old },
                    function () { console.log('函数2') },
                    function () { console.log('函数3') },
                    'print'
                ]
        },
        computed: {

        }
    }).mount('#app')
</script>
```

# 第四章

## 基本用法

v-model前面基本上已经用过了，这里主要做一些扩展

​	input标签有很多个类型，包括输入框，文本框，单选和复选框等等，这些标签用v-model其实都可以绑定，但是这里又涉及到value属性

```html
        <label for="agree">
            <input id="agree" type="checkbox" v-model="isAgree" value="hahaha" >同意协议
        </label>
```

​	input标签如果在form标签当中就是表单的一部分了，那么这里的单选框中，如果点击同意协议按钮，那value的值就会被表单收集，同样v-model也是这样的道理，只有点击复选框之后，才会被v-model跟新数值，值得注意的是，复选框要求绑定的值是数组

```html
        <label>
            <input type="radio" v-model="gender" value="male" > 男
        </label>
                <label>
            <input type="radio" v-model="gender" value="female" > 女
        </label>
```

​	单选框就更简单了，由for或者绑定的数值决定它们是不是一组，一组内只能选择一个选项，选择的选项会自动跟新到v-model绑定的数值当中

```html
<select v-model.lazy="fruit" mutilple >
    <option>1</option>
    <option>2</option>
    <option>3</option>
    <option>4</option>
</select>
```

下拉菜单栏和单选框差不多，其实就是选择哪个就绑定哪个，当然，可以给每个选项赋值一个值，这样就可以自定义传出的数据了

```html
<select v-model.lazy="fruit" mutilple >
    <option value=4 >1</option>
    <option value=3 >2</option>
    <option value=2 >3</option>
    <option value=1 >4</option>
</select>
```

比如这样，选择1选项，绑定fruit的数字就是4

## 修饰符

- number，将绑定的字符串转换为数字
- lazy，绑定input事件时，只有按Enter键才会触发更新
- trim，自动去除首尾的字符串

# 第五章

组件化，就是吧一个页面分成几个模块处理，每个模块独立处理自己的事情

## 注册全局组件

- 注册全局组件的前提是有两个组件，组件就是那个传入createApp的对象，这样的对象可以创建多个，我们叫它组件，每个组件都需要绑定一个模板，也就是组件对象里的template值，当创建好组件之后，需要将一个Vue实例作为根组件，然后这个实例可以添加其他组件，添加的方式就是component

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>title</title>
    <style>
        .comps-a,.comps-b{
            border: 1px solid #999;
            margin:3px;
        }
    </style>
</head>
<body>
    <div id="app"></div>
<!-- 根模板 -->
    <template id="my-app" >
        <component-a></component-a>
        <component-b></component-b>
    </template>

<!-- 模板1 -->
    <template id="component-a" >
        <div class="comps-b" >
            <input type="text" v-model.lazy="message">
            <h4>{{ message }}</h4>
        </div>
    </template>

<!-- 模板2 -->
    <template id="component-b" >
        <div class="comps-a" >
            <h4>{{ title }}</h4>
            <p>{{ desc }}</p>
            <button @click="btnClick" >按钮单击</button>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>
        // 根组件
        const app = {
            template:'#my-app',
            data:()=>{

            },
            methods:{

            },
            computed:{
              
            }
        }
        // 组件1
        const component_a = {
            template:'#component-a',
            data:()=>{
                return{
                    message:"Hello World",
                }
            },
            methods:{

            },
            computed:{
              
            }
        }
        // 组件2
        const component_b = {
            template:"#component-b",
            data(){
                return {
                    title:"我是标题",
                    desc:"内容显示区域....."
                }
            },
            methods:{
                btnClick(){
                console.log('按钮发生单击')
              }
            }
        }
        // 创建app
        const ap = Vue.createApp(app)
        // 添加组件
        ap.component("component-a",component_a)
        ap.component("component-b",component_b)
        ap.mount('#app')
    </script>

</body>
</html>
```

添加组件需要组件名称和组件对象

> ​    ap.component("component-a",component_a)
> ​    ap.component("component-b",component_b)

这一步只是在根组件中注册了两个组件而已

组测组件后就可以在根组件的组件模板当中调用组件了，调用的方式就是添加组件名的标签

> <template id="my-app" >
>     <component-a></component-a>
>     <component-b></component-b>
> </template>

## 注册局部组件

在应用程序启动时，全局组件就会全部注册完成，即使某些组件没有被使用，也会被注册

在组件对象中，除了data、methods、template、computed、watch之外，还有components，这里注册的组件只能在该组件下使用

注册的方式和component一样

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>title</title>
    <style>
        .comps-a,.comps-b{
            border: 1px solid #999;
            margin:3px;
        }
    </style>
</head>
<body>
    <div id="app"></div>
<!-- 根模板 -->
    <template id="my-app" >
        <component-a></component-a>
        <component-b></component-b>
    </template>

<!-- 模板1 -->
    <template id="component-a" >
        <div class="comps-b" >
            <input type="text" v-model.lazy="message">
            <h4>{{ message }}</h4>
        </div>
    </template>

<!-- 模板2 -->
    <template id="component-b" >
        <div class="comps-a" >
            <h4>{{ title }}</h4>
            <p>{{ desc }}</p>
            <button @click="btnClick" >按钮单击</button>
        </div>
    </template>

    <script src="../js/vue.js" ></script>

    <script>

        // 组件1
        const component_a = {
            template:'#component-a',
            data:()=>{
                return{
                    message:"Hello World",
                }
            },
            methods:{

            },
            computed:{
              
            }
        }
        // 组件2
        const component_b = {
            template:"#component-b",
            data(){
                return {
                    title:"我是标题",
                    desc:"内容显示区域....."
                }
            },
            methods:{
                btnClick(){
                console.log('按钮发生单击')
              }
            }
        }
                // 根组件
        const app = {
            template:'#my-app',
            data:()=>{
                return {
                    
                }
            },
            methods:{

            },
            computed:{
              
            },
            components:{
                'component-b':component_b,
                'component-a':component_a
            }
        }
        // 创建app
        const ap = Vue.createApp(app)
        ap.mount('#app')
    </script>

</body>
</html>
```

因为对象不能使用-作为名称，所以要添加双引号

# 第六章

在使用vue时，总是需要将组件分开成几个文件进行更好的管理，但是，如果直接使用js分开，并不是最好的办法，官方推荐使用.vue文件，将每个组件分开，但是浏览器并不认识.vue文件，所以需要将.vue文件的各个组件重新包装成js文件，这个时候使用vite是比较方便的

## vue create

下载nodejs会包含npm，npm是包管理器，也就是管理别人编写的js文件，比如vue就是其中的一种，首先我们要创建vue项目，就需要vue，所以用npm下载vue在全局当中

```
npm install @vue/cli -g
```

-g就是全局的意思

然后再终端创建vue项目

```powershell
vue create <项目名称>
```

这个时候会在当前目录下面创建一个名字为项目名称的目录

目录下面有这些文件

![image-20241120000000784](https://db.xinghai.ink/Typora/173498701076498.png)

- node_models，用来存放第三方包的文件，也就是用npm install 不添加-g的时候，包会下载到这里
- public，项目的一些资源，这些资源并不会参与打包，打包的意思就是将vue文件打包成js文件这样，打包会生成一个新的文件夹
- src，用来存放项目的所有代码的目录
  - assets，项目的资源，包括图片，字体，全局样式等
  - component，这个就是用来存放组件的地方，里面的每一个.vue文件都是一个组件，
  - App.vue,项目的根组件
  - main.js程序的入口文件，也是打包的入口文件

## create-vue

推荐使用create-vue来代替vue的脚手架，因为他快

**下载create-vue**

```
npm install create-vue -g
```

这里同样是全局下载

**创建项目**

```
create-vue
```

没错，就是这么简介，然后根据提示输入名称和选择选项就好了

**安装依赖**

```
npm install
```

进入到项目目录里面需要安装依赖，虽然create-vue会添加支持vite的配置和文件，但是他不会安装vite，所以需要安装依赖

**启动项目**

```
npm run dev
```

dev的意思就是用vite去启动service

**打包**

在服务器中，服务器配置的文件其实就是这个项目的根目录，所以项目都会以根目录开始的形式编写路径，但是如果这样编译的话，在本地是打不开的

需要在vite.config.js中配置base为'./'，也就是，当前目录

![image-20241120011038976](https://db.xinghai.ink/Typora/17349870184595222.png)

配置完成后输入打包命令

```
npm run build
```

然后再目录下，找到dist的index，然后打开

![image-20241120011143721](https://db.xinghai.ink/Typora/1734987025409743.png)

好了，就这样

# 第七章

## 组件嵌套

删除component和assets目录，因为用不到，然后修改App.vue

```html
<template>
    <div class="message" @click="Message">{{ message }}</div>
    <Header></Header>
    <Main></Main>
    <Footer></Footer>
</template>




<script>
import Header from './Header.vue'
import Main from './Main.vue'
import Footer from './Footer.vue'

export default {
    name: 'name',
    components: {
        Header,
        Main,
        Footer
    },
    data() {
        return {
            message: 'hello Word',
        }
    },
    methods: {
        Message(event){
            console.dir(event.target)
        }
    },
}
</script>



<style>
.message {
    color: rgb(255, 0, 0);
    width:100px;
    margin:100px auto;
}
</style>
```

先看这部分代码，export deault的意思就是，如果有别的文件用import语句引用这个文件，那么就会默认返回default的对象

上面使用了三个import语句，分别引入了三个vue文件，也就是三个组件，然后三个组件被局部注册到了根组件当中

## 组件样式特性

在组件当中，如果直接使用`style`标签，那么设置的标签就是全局的，但是，大多数时候，我们都希望我们设置的标签是局部的，仅仅在该组件中生效，这时，可以在`style`标签后加上scoped标记

```html
<template>
    <div class="header" >
        <h4>Header</h4>
        <h4>NavBar</h4>
    </div>
</template>




<script>
export default {}
</script>



<style scoped>
.message {
    color: rgb(255, 0, 0);
    width:100px;
    margin:100px auto;
}
</style>
```

这样，style标签只在当前组件生效，其实原理很简单

在css样式有这样的表达式

```css
div[nana]{}
```

样式表示，定位有nana属性的div标签，无论nana属性是否有值

在Vue当中，如果设置了scoped标记，vue会给应该生效的标签自动添加一个唯一的属性，例如

![image-20241120103658909](https://db.xinghai.ink/Typora/17349870328049679.png)

这个标签的`data-v68aa8fa7`就是vue添加的，这样就能隔离组件之间的样式

## 局部样式泄露

组件中会包含子组件，而子组件的根节点，也就是根标签会收到父标签和子标签的样式的共同影响，其实这是故意这样设计的，因为样式之间本来就会影响子节点，我们可以这样认为，子组件的根标签任然会被父标签的样式影响

- 消除影响的方法就是，不要给子组件的根标签设置样式，这个很好解决

- 但是还有一种情况，就是我需要父组件影响子组件，但是如果根标签有很多个的话，那父标签就不能影响子标签

  - ```html
    <template>
        <div class="asdf">abc</div>
        <div class="asdf">abc</div>
    </template>
    ```

    例如这样，那父组件就无法影响子组件，这是因为默认情况下子组件只能会有一个，但如果设置多个，vue就会给他们的上一层设置一个标签，但是在渲染的时候会去除这个标签，就好像真的是两个根节点似的，但是对于父节点来说，子组件的根节点只有那个vue创建的虚拟标签，但是那个标签无法记录css，class等样式信息，这样，也就无法影响到子节点了

## 父子组件通信

子组件获取父组件使用props属性，这个属性在模板对象中

```html
<template>
    <div class="msg" >
        <h4>{{ title }}</h4>
        <h4>{{ content }}</h4>
    </div>
</template>
<script>
export default {
    props:['title','content'],
}
</script>
```

例如，这里的props就是从父组件中获取title和content属性

当然，前提是父组件需要传入这些参数给子组件

```html
<template>
    <HelloWord :="message" ></HelloWord>
    <HelloWord :title="title" :content="content" ></HelloWord>
    <HelloWord title="我是标题" content="我是内容" ></HelloWord>
</template>




<script>
import HelloWord from './HelloWorld.vue'
export default {
    components: {
        HelloWord
    },
    data() {
        return {
            title:'我是标题,title',
            content:'我是内容,content',
            message: {
                title:'我是标题,message.title',
                content:'我是内容,message.content'
            },
        }
    },
}
</script>
```

直接在标签属性当中传递参数和值

**传递对象**

具体来说，用列表的方式传递对象，如果父组件没有给参数的话，那就直接显示空值，那用对象的方式就是为了解决这种情况，增加一些限制

```html
<template>
    <div class="msg" >
        <h4>{{ title }}</h4>
        <h4>{{ content }}</h4>
    </div>
</template>
<script>
export default {
    props:{
        title:String,
        content:{
            type:String,
            required:true,
            default:'hahaha'
        }
    }
}
</script>
```

- 传递了两个参数，分别是title和content，title设定了必须给字符串类型，content设置了，类型为字符串，必须传递字符，不然会出现警告，如果没有传递，则使用默认值
- type:接收的数据类型，如果不匹配则会警告，可以用数组接收多个类型
- require，是否为必须传入的参数，如果设置为true，而且没有传入就会出现警告
- default，参数没有被传入时的默认值
- valudator，传入一个函数，默认会给函数传入value参数，函数返回true或者false，用来验证数值是否合规

## 插槽

在我们插入组件的时候，可以发现组件是一个双标签，但是我们往标签里面插入数据，并不会显示在组件当中，其实这里输入的数据是需要在组件里面提前定义插槽的，插槽的标签是`<slot></slot>`，在组件中定义了这个，那调用组件的收往标签里插入的数据就会放入在这里

```html
<template>
    <div class="my-button" >
        <button>custom button</button>
        <slot></slot>
    </div>
</template>
```

调用时

```html
<template>
    <div class="app" >
        <MySlotCpn><Mybutton>adf</Mybutton></MySlotCpn>
        <MySlotCpn>插槽2</MySlotCpn>
        <br>
        <MySlotCpn>
            <h4>haha</h4>
        </MySlotCpn>
    </div>
</template>
```

这样，输入在`<MySlotCpn></MySlotCpn>`的内容，就会插入在`<slot></slot>`当中

### 具名插槽

一个组件当中，可以有很多个插槽，默认情况下，输入多个插槽都会使用一个内容显示，那如果，需要不同的插槽显示不同的内容，在默认的插槽标签中，会自动代一个name属性`<slot name='default' ></slot>`，我们默认给组件的值就插入到默认的插槽当中，如果需要将特定的值，放入特定的插槽，就需要修改name的值

```html
    <div>
    <slot name="slot1" >插槽1</slot>
    <slot name="slot2" >插槽2</slot>
    </div>
```

在使用组件时，需要使用`<template>`,然后带上v-slot，例如`<template v-slot:'slot'></template>`

```html
<template>
    <div class="app" >
        <MySlotCpn>
            <template v-slot:slot1 >abc1</template>
            <template v-slot:slot2 >abc2</template>
        </MySlotCpn>
    </div>
</template>
```

在使用过程中,通过v-slot表达式指定`<template></template>`的内容插入到哪个插槽

例如上方的abc1，就显示在插槽1，abc2，就显示在插槽2

### 动态插槽名

动态名插槽的原理就是，插槽的名称通过夫组件传入，然后子组件通过props接收到后绑定在<template></template>上

例如

```vue
<template>
    <div>
    <slot :name="slot1" >插槽1</slot>
    <br>
    <slot :name="slot2" >插槽2</slot>
    </div>
</template>




<script>

export default {
    props:{
        slot1:{
            type:String
        },
        slot2:{
            type:String
        }
    }
}
</script>
```

### 作用域插槽

如果一个文件有很多个相同名称的插槽，比如 多个带有`name="name"`属性的插槽,那么再父组件往插槽中放入数据，vue就会将数据放入每一个插槽中，但是如果放入的数据和插槽的属性有关，那情况就不一样了

```vue
<template>
  <div>
    <slot name="name" key="1" ></slot>
    <slot name="name" key="2" ></slot>
    <slot name="name" key="3" ></slot>
    <slot name="name" key="4" ></slot>
    <slot name="name" key="5" ></slot>
    <slot name="name" key="6" ></slot>
    <slot name="name" key="7" ></slot>
  </div>
</template>
```

例如如下插槽，名称一样，但是key属性不同

现在回到父组件

```html
<template>
<div>
  <DD :names="names">
      <template #name="slotProps" >
        <span>{{ slotProps }}</span>
      </template>
  </DD>
</div>
</template>
```

在组件中，`#name="slotProps"`是`v-slot:name:"slotProps"`的缩写，在前面的知识点提到过，v-slot是用于指定该template属于哪个插槽

这里继续拓展以下语法，v-slot:name:"slotProps"的意思就是将插槽名称为name的节点中的所有属性和值组成的对象，放入到slotProps中

这里看一下运行结果

![image-20241126210901844](https://db.xinghai.ink/Typora/17349870409362245.png)

可以看到，每个插槽虽然名称一样，但是对应的节点的属性有可能是不一样的，所以我们可以利用这一点，让插槽里的内容显示插槽的属性的某个内容

```vue
<template>
<div>
  <DD :names="names">
      <template #name="slotProps" >
        <span>{{ slotProps.key }}</span>
      </template>
  </DD>
</div>
</template>
```

效果

![image-20241126211045279](https://db.xinghai.ink/Typora/17349870467520888.png)

拓展

```vue
<template>
  <div>
    <slot v-for="key in 9" name="name" :key ></slot>
  </div>
</template>
```

可动态显示列表

如果插槽的名称为默认，在父组件中可将`v-slot=default="slotProps"`简写成`#="slotProps"`

```vue
<template>
<div>
  <DD :names="names">
      <template #="slotProps" >
        <span>{{ slotProps.key }}</span>
      </template>
  </DD>
</div>
</template>
```

# 第八章

## 动态组件

一般来说，在父组件中插入子组件可通过插件名称以标签的形式插入，在某些场景下需要选择性的选择显示某个组件，这时候可以用component标签，例如

```
<component is="Home" ></component>
. . . . . .
export default {
    components: {
        About,
        Catgory,
        Home
    }
    }
```

这里表示，在component标签当中插入下面components里的Home的组件

is用于指定组件，淡然可以用v-bind绑定变量

```vue
<template>
    <div class="btnd">
        <button 
            v-for="(value, key) in tabs" 
            :key
            @click="itemClick(value)" 
            :class="{ btnactive: currentTab === value }" 
            class="btn"
        >
            {{ value }}
        </button>
        <component :is="currentTab" ></component>
    </div>
</template>

<script>
import About from './About.vue'
import Catgory from './Catgory.vue'
import Home from './Home.vue';

// 名称首字母大写可以用小写替换，但是小写不能用大写替换
export default {
    components: {
        About,
        Catgory,
        Home
    },
    data() {
        return {
            tabs: ['home', 'about', 'catgory'],
            currentTab: 'home'  // 确保初始值为 'home'
        }
    },
    methods: {
        itemClick(value) {
            this.currentTab = value;  // 确保点击按钮时更新 currentTab
            console.log(value);
        }
    }
}
</script>

<style scoped>
	/* 权重为10 */
    .btnd .btn {
        border: none;
        margin-right: 10px;
        background: #e7e6e624;
        width: 80px;
        border-bottom: 2px solid #ddd;
        height: 30px;
    }
    /* 权重为10 + 10 */
    .btn.btnactive {
        border-bottom: 2px solid red ;
        color:red;
    }
</style>
```

### 组件传参

如有传参的需要，可以直接往component传入props需要的参数

```vue
    <component :is="currentTab"
    name="codeWay"
    :age="18"
    @pageClick="(venv)=>{console.log(venv)}"
    ></component>
```

### keep-alive

默认情况下，使用temponent标签切换标签后，之前的标签会被销毁，当重新切换回来相当于重新注册，那么之前在组件中保存的数据也就会重置，这种情况下，可以使用keep-alive标签保存各个组件的状态，而不是被销毁

```vue
<template>
    <div class="btnd">
        <button v-for="(value, key) in tabs" :key @click="itemClick(value)" :class="{ btnactive: currentTab === value }"
            class="btn">
            {{ value }}
        </button>
        <keep-alive>
            <component :is="currentTab" name="codeWay" :age="18" @pageClick="(venv) => { console.log(venv) }"></component>
        </keep-alive>
    </div>
</template>
```

使用方法就是直接在component前面加入keep-alive标签

### include

如果只需要某些组件保留状态，那就可以在keep-alive中加入include参数，参数接收字符串、列表等类型，只有名称匹配的组件才会被保存，这里的名称和组件的变量无关，而是需要保留的组件的name属性有关

```vue
<template>
  <div class="btnd">
    <button v-for="(value, key) in tabs" :key="key" @click="itemClick(value)"
      :class="{ btnactive: currentTab === value }" class="btn">
      {{ value }}
    </button>

    <keep-alive include="HH">
      <component :is="currentTab" name="codeWay" :age="18" @pageClick="(venv) => {
          console.log(venv);
        }
        " />
    </keep-alive>
  </div>
</template>

<script>
import about from "./About.vue";
import Catgory from "./Catgory.vue";
import Home from "./Home.vue";

export default {
  components: {
    about,
    Catgory,
    Home,
  },
  data() {
    return {
      tabs: ["home", "about", "Catgory"], // 注意数组中应使用组件名称
      currentTab: "home", // 初始组件为 Home
    };
  },
```

- 这里只是一部分的代码，看最上方的include接收了HH但是在这个文件中并没有HH变量，其实这个时Home组件的名称，在这里Home只是变量，实际上组件的名称为HH

```vue
<!-- Hone.vue文件 -->
<script>
export default {
  name: "HH",
  props: ["name", "age"],
  emits: ["pageClick"],
  data() {
    return {
      c: 0,
    };
  },
};
</script>
```

## 8.2   异步组件

在vue3开发中，经常用到异步加载组件，异步组件的加载过

<h3>vue3异步组件</h3>

vue的异步组件通过import函数动态导入vue资源，然后通过vue的defineAsyncComponent函数将资源转换成vue组件

home组件

```vue
<template>
    <div class="home">
        <h1>Welcome to Home Page</h1>
        <p>This is a simple Vue component.</p>
    </div>
</template>

<script>
export default {
    name: "Home",
};
</script>

<style scoped>
.home {
    text-align: center;
    margin-top: 20px;
}
</style>
```

asyncCategory.vue组件

```python
<template>
    <div class="async-category">
        <h4>{{ message }}</h4>
    </div>
</template>

<script>
export default {
    data() {
        return {
            message: "AsyncCategory异步组件"
        }
    }
}
</script>
```

app根组件

```python
<template>
    <div class="app" >
    <home></home>
    <async-category></async-category>
</div>
</template>

<script>
import home from './home.vue';
import {defineAsyncComponent} from 'vue'
const AsyncCategory = defineAsyncComponent(()=>{ return import("./AsyncCategory.vue")})

export default{
    components:{
        home,
        AsyncCategory
    }
}
</script>


```

通过执行后可以在网络中看到，网络单独的加载了AsyncCategor组件

![image-20250428235306856](https://db.xinghai.ink/Typora/17458555890579505.png)



# 关于flex布局

- flex是一个弹性布局，任何一个容器都可以指定为flex
- 当我们设置父元素为flex布局以后，里面的float、clear、vertical-align会失效
- 当我们设置成弹性布局之后将不是原来的行级元素和块级元素的模式了，而是全新的flex模式
- 采用flex布局的元素叫做flex容器，他所有的子元素都是成员容器，成为flex项目
- 容器默认是横向排列的
- 既然分为容器和项目，那就有些属性需要给容器添加，有些熟悉是给项目添加的

## 容器常用属性

- flex-direction:设置主轴方向
- justify-content:设置主轴上的子元素排列方式
- flex-wrap:设置子元素是否换行
- align-center:设置侧轴上的子元素的排列方式
- align-items:设置侧轴上的子元素的排列方式
- flex-flow符合属性

## flex-directon

flex分为主轴和侧轴方向，也就是x轴和y轴,可以通过flex-direction改变主轴方向

如果flex-direction设置为column（默认），那么侧轴就默认被沾满

