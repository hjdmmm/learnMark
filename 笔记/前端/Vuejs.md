# Vuejs简介

Vuejs是一套构建用户界面的框架，它只关注视图层的内容，他是前段的主流框架之一

前端三大主流框架：Angular.js，React.js，Vue.js

前端框架主要负责MVC中V的这一层，主要工作就是和界面打交道，主要是用来对页面中的数据进行处理，以及制作前端页面相关的特效及动画

## 使用原因

在实际项目开发中，不论是做前段开发还是后端开发，使用框架技术是最佳的提高效率的方法

另外使用vuejs来做前段框架，对于处理数据的方面可以完全的替换掉原有的dom操作理念(之前我们常用的原声js以及jQuery类库)，通过Vuejs框架提供的指令，前段开发人员不再关心dom是如何渲染的，可以有更多时间去关注业务逻辑本身。

Vuejs作为先进最火爆的前端开发框架，学习后可以有效地提高就业的价值

## 版本1和2

Vuejs当今应用最常用的两个版本，分别是Vue1.js以及Vue2.js

版本2在版本1的基础上进行了大量的改动，所以二者在概念和语法上有很大区别，新项目使用Vue2

# MVVM

MVVM是前端视图层的分层开发思想。主要是用来将每一个页面分成M，V，MV这三种组件。这三个组件在前端开发中分工协作，分工明确

M表示页面需要处理的数据这一部分；VM整体调度者，分割了M和V，当V想要获取或者传递数据M的时候，使用VM来做调度；V表示页面中，用来展示页面的这一部分HTML代码

其中，VM是MVVM的核心，是因为VM是M和V之间的一个整体的调度者

我们所要学习的Vue.js就是通过Vue.js框架来创建VM这一组件，为M和V来进行服务

# 指令属性

## v-cloak

使用v-cloak主要是为了解决插值表达式的闪烁问题

使用插值表达式的问题：页面加载过程中，在页面中的{{}}插值表达式首先会被页面认可为是html元素中的实在存在的内容。所以浏览器会首先将{{}}展现在页面上。页面加载完毕后，插值表达式才会真正地转变为动态赋予的值，这就会造成一种现象，如果将来终端在访问服务器的过程中，网速较慢，那么我们的{{}}会首先展现出来，{{}}展现出来之后，会一闪而过，这就是所谓的插值表达式的闪烁问题

```html
<!--用样式隐藏控件-->
<style>
    [v-cloak]{
        display: none;
    }
</style>
<!-- 给具体控件绑定v-cloak -->
<p v-cloak>{{str1}}</p>
```

## 为页面渲染值的方式

### 插值表达式

```html
<div>
    <p>######{{str1}}######</p>
</div>

<script>
	var vm = new Vue({
        el : "#app"
        data : {
        	"str1" : "aaa"
    	}
    })
</script>
```

对于元素中已经存在的值，只有插值表达式能够将原有的值保留，在原有的已经存在的值的基础上添加动态数据(插值表达式名称的由来)

插值表达式会出现页面闪烁的现象

使用插值表达式与v-text一样，html代码不会得到解析

### v-text

```html
<div>
    <p v-text="str1">######</p>
</div>

<script>
	var vm = new Vue({
        el : "#app"
        data : {
        	"str1" : "aaa"
    	}
    })
</script>
```

会提前将标签中原有的内容清空

不会出现页面闪烁的现象

v-text = innerText

### v-html

```html
<div>
    <p v-html="str1">########</p>
</div>

<script>
	var vm = new Vue({
        el : "#app"
        data : {
        	"str1" : "aaa"
    	}
    })
</script>
```

会提前将标签中原有的内容清空

不会出现页面闪烁的现象

v-html = innerHTML

因为实际使用中不应该让用户看到任何html代码，所以实际上用v-html多一些

## v-bind

v-bind是Vuejs中，提供用于绑定属性的指令

```html
<div id="app">
    <!-- 以下input标签对value属性中的值，使用vm对象，由vm对象将data中的信息动态的赋予到该value属性中，必须使用指令属性v-bind完成 -->
    <input type="text" v-bind:value="str1"/>
    
    <!-- v-bind复用率太高，所以可以将其省略不写，只写: -->
    <input type="text" :value="str1"/>
    
    <!-- v-bind还支持字符串拼接 -->
    <input type="button" value="submit" :title="str1"+"haha"/>
</div>

<script>
	var vm = new Vue({
        el : "#app",
        data : {
            "str1" : "aaa"
        }
    })
</script>
```

## v-on

```html
<div id="app">
   <input type="button" value="点击按钮" v-on:click="fun1"/>
    
   <!-- v-on的复用率也很高 可以用@来简化-->
   <input type="button" value="点击按钮" @click="fun1"/>
</div>
    
<script>
	var vm = new Vue({
        el : "#app",
        methods : {
            fun1(){
                alert("abc");
            }
        }
    })
</script>
```

### 事件修饰符

这些修饰符可以多个联合使用，多点几次就行了

1. .stop

   使用.stop来对事件的冒泡机制进行阻止。js中事件冒泡指的是，在触发内层元素事件的同时，也会继续触发外层元素的事件(因为外层元素包裹了内层元素)。在实际开发中，几乎不会用到冒泡机制。

   ```html
   <div id="app" style="width:200px;height:200px;background-color:red" @click="fun1">
       <div style="width:100px;height:100px;background-color:blue" @click.stop="fun2">
       </div>
   </div>
   ```

2. .prevent

   阻止超链接默认的行为。所谓默认的行为指的是超链接中的href属性链接。在实际开发中，不仅仅只是按钮需要我们绑定事件来控制行为，超链接的使用也是我们要遵循这种自己绑定事件触发行为的方式，所以在a标签中的href链接旺旺要被我们以特殊的方式处理掉

3. .capture

   ```html
   <div id="app" style="width:200px;height:200px;background-color:red" @click.capture="fun1">
       <div style="width:100px;height:100px;background-color:blue" @click="fun2">
       </div>
   </div>
   ```

   使用的是外层div套内层div的例子，其中内层div没有阻止冒泡，加了.capture修饰，先触发的是外层的div，后触发内层div，提高了外层优先级

4. .self

   ```html
   <div id="app" style="width:200px;height:200px;background-color:red" @click="fun1">
       <div style="width:100px;height:100px;background-color:blue" @click.self="fun2">
           <input type="button" value="按钮" @click="fun3">
       </div>
   </div>
   ```

   也是阻止事件的冒泡机制，但是是阻止自身的冒泡

5. .once

   只触发一次事件处理函数

   ```html
   <a href="http://baidu.com" @click.prevent.once="fun1">百度</a>
   <!--第一次点击时能触发@click.prevent事件-->
   <!--第n(n>1)次点击时不能触发@click.prevent事件-->
   <!--相当于只能触发一次@click事件-->
   ```

## v-model

v-bind只能实现数据的单向绑定，从模型(M)绑定到视图(V)，使用VM将数据去渲染视图，但是无法从V到M

双向数据绑定：不仅仅只是从M取到数据渲染V，还可以从V的变化动态更新M的值。在实际开发中，不仅仅只是将模型准确的渲染到视图中，视图中数据的变化，更需要模型去进行有效的记录

使用v-model可以对数据进行双向的绑定操作，由于记载页面元素值的需求都是在表单中进行的，所以v-model只能运用在表单元素中(input, select, textarea)

```html
<input type="text" v-model:value=""/>
```

# 使用class样式

使用vuejs控制样式，会使样式变化更加灵活

1. class样式的使用

   ```html
   <!--传递一个class样式的数组，通过v-bind做样式的绑定-->
   <span :class="['style1', 'style2', 'style3', 'style4']">Hello style</span>
   
   <!--通过三元运算符操作以上数组-->
   <span :class="['style1', 'style2', 'style3', flag?'style4':'']">Hello style</span>
   
   <!--json格式的操作以上数组，比三目运算符可读性好-->
   <span :class="['style1', 'style2', 'style3', {'style4':flag}]">Hello style</span>
   
   <!--全部都用json格式-->
   <span :class="{style1:true, style2:true}">Hello style</span>
   
   <!--通过以直接模型M的形式做样式渲染-->
   <span :class="{style1:true, style2:true}">Hello style</span>
   
   <script ...>
   	...
       	data : {
               flag = true,
               
   			//这样使用必须直接将具体的boolean值结果(true/false)赋值，不能以this.模型的形式来做引用，以避免data中的数据互相引用
               myStyle : {style1:true}
           }
   </script>
   ```

   

   

2. style样式补充

   在实际开发中，对于style样式的使用，没有class使用广泛，通常style属性仅仅只是对个别指定元素的样式进行的进一步补充使用

   ```html
   <!--在写color这样的样式属性的时候，由于仅仅只是一个单词，所以不需要加引号，开发中大多数样式都是有横杠的(font-style)，必须包含在引号中-->
   <span :style="myStyle1"></span>
   <span :style="[myStyle1, myStyle2]"></span>
   <script ...>
   	...
       data : {
           myStyle1 : {color : 'red', 'font-size' : '30px'},
           myStyle2 : {'font-size':'italic'}
       }
   </script>
   ```

   

# v-for

v -for="元素 in 数组"

v -for="(元素, 下标) in 数组"

v -for="(键, 值) in 对象"

v -for="(键, 值, 下标) in 对象"

v -for="元素 in 整型数字"

## key属性

在实际开发中，使用v-for仅仅只是将元素遍历出来，并展现在页面上。如果需要指定遍历到的某个元素，那么视图并没有为我们提供一个有效的辨识指定元素的方案，所以在遍历元素时，需要为每一个遍历出来的元素做一个有效的标识，这个标识就是该元素在该页面的唯一标识。所以我们应该在遍历元素时都加上key

key属性值必须是一个数值或一个字符串，不能是对象

key属性的应用，必须搭配绑定v-bind指令，否则不会生效

key属性所赋的值，必须是记录的唯一标识，通常使用id

# v-if和v-show

```html
    <p v-if=flag>
        显示段落1
    </p>
    <p v-show=flag>
        显示段落2
    </p>

<!--当flag为true时都是-->
<p>显示段落1</p>
<p>显示段落2</p>

<!--当flag为false时-->
<!-- <p>显示段落1</p> 这一行直接被删除了 -->
<p style="display: none;">显示段落2</p> <!--这一行是被添加样式，隐藏起来-->
```

在实际中，一般需求情况使用v-if，但如果需要对元素展现与否频繁切换，就用v-show展现或者隐藏元素

# 过滤器

过滤器是一个通过输入数据，能够及时对数据进行处理并返回一个数据结果的简单函数。

在实际项目开发中，根据实际的需求，可以自己编写所需的过滤器

过滤器经常在数据所需的格式化使用，例如：字符串的格式化，日期时间的格式化等

过滤器最大的作用就是体现其复用性，如果我们在前端处理的某些文件信息每一次都需要经过重复的特殊处理，那么我们一定是要编写一个过滤器来使用

在开发过程，可以连续使用多个过滤器

## 全局过滤器

全局过滤器指的是所有vm对象都能共享使用的过滤器

过滤器能够使用在两个地方：插值表达式/指令属性

过滤器语法:管道符(|)

过滤器在插值表达式的使用：{{内容|过滤器}}}

```html
<!--定义字符串变为大写的过滤器及其使用-->
<p>{{str1 | ucase}}</p>
<script>
	Vue.filter("ucase", function(value){
    	value = value.toUpperCase();
    	return value;
	})
</script>
```

## 私有过滤器

私有过滤器指在指定的vm对象中来定义过滤器，只在指定的vm对象生效

```javascript
var vm = new Vue({
    filters : {
        filter1 : function(value){}
    }
})
```

全局过滤器和私有过滤器重名时，优先使用私有过滤器

# 指令

指令与属性相似，是对指定元素样式或行为的赋予。

我们可以在实际项目开发中自定义一些我们所需的指令来有效的管理元素

## 自定义全局指令

在页面中的自定义全局指令，可以为每一个vm对象中的元素提供服务，只要vm中的标签引用了全局指令，那么一定会即时生效，一般情况下，我们普遍做的都是自定义全局指令来管理元素。

自定义指令需要经常搭配vuejs中的钩子函数来进行操作

```html
<input type="text" v-dt1="'green'"/><!--如果不加单引号，会去寻找el的data中的数据-->
<script type="text/javascript">
	/*
		directive提供两个参数
		参数1：关于指令的名称，在定义的时候前面不需要加"v-"前缀，但是在使用的时候一定要在"v-"前缀
		参数2：json对象，在这个对象身上，有一些指令相关的函数，这些函数可以在特定的阶段，执行相关的
		操作(钩子函数)
		在未来的项目开发中：
		使用bind()函数来操作 元素的样式(css)
		使用inserted()函数来操作 元素的行为(js)
	*/
    Vue.directive("dt1", {
        //这三个函数与vuejs对象的生命周期密切相关的函数，el对象同时也是一个原生的js对象(dom对象)
        
        //bind()函数：每当指令绑定到该元素上的时候，会立即执行这个bind()函数，该函数只执行一次
        //binding参数，是在元素使用指令的时候，为函数传递的一个具体的值，通过赋值的形式为元素来进行操作
        bind: function(el, binding){
            //将指定元素的文本信息改变颜色
            el.style.color=binding.value;
        },
        
        //inserted()函数：表示元素插入到dom中的时候，会执行该函数，该函数只会执行一次
        inserted: function(el){
            //focus()如果写在bind，会因为dom元素还没有插入到dom树中而无效
            el.focus();
        },
        
        //update()函数，当vuejs中的元素更新的时候，会触发该函数
        update: function(el){
            
        }
    })
</script>
```

## 自定义私有指令

```html
<p v-mydt>
    haha
</p>
<script>
    var vm1 = new Vue({
        directives:{
            "mydt":{
                bind : function(el){
                    el.style.color = "red";
                }
            }
        }
    })
</script>
```

# vuejs对象的生命周期

## 创建阶段

1. new Vue()：创建一个Vue实例
2. Init( Events&Lifecycle )：步入到对象初始化的前期阶段，表示通过以上代码我们创建了Vuejs对象，此时在新建的对象身上，具备了一些生命周期相关的函数(生命周期的钩子函数)和默认事件，但是其他的相关组件还没有被加载(data，methods，filter等)
3. Init( injections&reactivity )：该阶段是对象初始化的后期阶段，执行其的方式是调用created()，在该函数中，data和methods都已经被初始化好了，也就是说，最早可以在created()中操作data，methods
4. Init对象初始化阶段执行完毕后，通过对元素以及模板进行判断，系统开始编辑模板，将Vue代码中的指令进行执行，然后在内存中生成一个编辑好的模板字符串，最终将该模板字符串渲染为内存中的DOM。但是此时仅仅只是在内存中渲染好模板，并没有将模板挂载到页面上，该阶段执行完毕后执行beforeMount()方法
5. create vm：该阶段是将内存中编译好的模板，替换到浏览器的页面中，该阶段的进行完毕后，进行mounted()方法，只要执行完了mounted()方法，就表示整个Vue对象已经初始化完毕了，正式进入运行阶段，如果要通过某些插件操作页面上的DOM节点，最早是要在mounted()中执行

## 运行阶段

Virtual DOM：该阶段会根据data中的最新数据，重新渲染出一份最新的DOM树，当最新的内存DOM树被更新后，会把最新的DOM树重新渲染到页面中去，这时候就完成了使用模型Model去渲染视图View的过程。该阶段的执行会使用到两个函数beforeUpdate()和updated()这两个函数，会根据data数据的变化，可重复执行多次。当beforeUpdate()方法执行的时候 ，页面中显示的还是之前的数据，但是data中保存的是新数据，页面没有与data同步。当updated()执行的时候，页面已经和data同步了

## 销毁阶段

1. Teardown：该阶段为对象销毁的阶段，当对象实例运行完毕后，如果达到了对象销毁的条件，执行beforeDestroy()，该函数的执行正式标志着对象从运行阶段进入销毁阶段。当beforeDestroy()执行的时候，data、methods等组件还处于可用状态，该函数执行完毕后，对象正式销毁。
2. Destroyed：该阶段为对象销毁后的阶段，该阶段会执行destroyed()，当该函数执行的时候，对象已经被销毁了，里面的data，methods等组件也就不能使用了

## 钩子函数

beforeCreate()：不能用data和methods

created()：已经可以用data和methods了

beforeMount()：会出现{{str1}}

mounted()：会出现aaa

beforeUpdate()：永远慢一步，已经改为aaa1还是aaa

updated()：跟上进度，改为aaa1就是aaa1

beforeDestroy()：data、methods还是可以使用的

destroy()：不能用各种组件了

# ajax请求

Vuejs本身不支持发送ajax请求，需要使用插件来实现

vue-resource插件，axios插件

## vue-resource

```javascript
//发出ajax请求，取得学生信息，在页面中局部刷新学生信息
getStudent(){ //"01"是servlet别名
    //后面的json属性是通过请求(request)发送的参数，但是在vue-resource中get方法不支持这样传参，只能加在请求资源后
	this.$http.get("01?name=zs").then(function(data){
    //data是收到的数据(json对象)
    //要加一个body
	this.id = data.body.id;
	this.name = data.body.name;
	this.age = data.body.age;
	})
}

getStudent(){ //"01"是servlet别名
    /*
    post方式传参：
    手动发起的post请求，默认没有表单格式，有些服务器处理不了
    我们需要通过post的第三个参数，{emulateJSON:true}设置，提交的内容类型就设置为了普通表单的格式传递参数
    */
	this.$http.get("01, {"name":"zs"}, {emulateJSON:true}).then(function(data){
    //data是收到的数据(json对象)
    //要加一个body
	this.id = data.body.id;
	this.name = data.body.name;
	this.age = data.body.age;
	})
}
```

## axios

axios的形式是一个基于Promise的HTTP请求客户端，用来发送请求，该形式是vue2.0官方推荐的方式

```javascript
getStudent(){
  //将Vue对象传入axios中
  var _this = this;
  axios({
  method : "get",
  url : "02", 
  //get可以这样传参
  params : {"name" : "bbb"}
  }).then(function(result){
 	//这样写是无法赋值的，原因在于this在vue中指向vue对象，但是在axios中指向的是axios对象，也就是undefined
  	this.id = result.data.id;
  	this.name = result.data.name;
  	this.age = result.data.age;
    //这样才可以
    _this.id = result.data.id;
  	_this.name = result.data.name;
  	_this.age = result.data.age;
  })
}

getStudent(){
  //将Vue对象传入axios中
  var _this = this;
  axios.post(
  	"02", 
    //post不能这样传参
    //params : {"name" : "bbb"}
    //应该这样传
    "name=aaa"
  ).then(function(result){
 	//这样写是无法赋值的，原因在于this在vue中指向vue对象，但是在axios中指向的是axios对象，也就是undefined
  	this.id = result.data.id;
  	this.name = result.data.name;
  	this.age = result.data.age;
    //这样才可以
    _this.id = result.data.id;
  	_this.name = result.data.name;
  	_this.age = result.data.age;
  })
}
```

# 跨域请求

同源：同源指的是在一般情况下，浏览器发出请求访问的资源都是在相同的协议，域名和端口号下的，这样的请求就是默认同源策略的访问。

由于浏览器的同源策略，凡是发送请求url，域名，端口号其中任意一个与当前页面地址不同，即为跨域

在实际开发中，使用的当前页面有可能会发出这样的请求，访问的是非同源的资源，那么我们就需要进行跨域处理

常用与分布式服务器处理

## 常用处理方式

## 代理方式

代理用于将请求发送给后台服务器，通过服务器来发送请求，然后将请求的结果传递给前端，通过nginx代理来实现操作

优点：跨域服务稳定

缺点：在使用到跨域处理的时候，必须事先搭建nginx代理服务环境，比较麻烦

## CORS方式

CORS是W3C标准的方式，通过在web服务器端的设置

响应头Access-Control-Alow-Origin来指定哪些域可以访问本域的数据

优点：使用简单，支持基于HTTP协议的所有请求方式

缺点：跨域服务响应较慢

## jsonp方式

通过动态插入一个script标签，浏览器对script的资源引用没有同源限制，同时资源加载到页面后立即执行

优点：使用简单，跨域服务响应快，获取的数据是我们最常用的json格式的数据

缺点：只能发送get请求，无法发送post请求



由于在开发中发出跨域请求的目的通常是为了取得指定的资源数据，所以一般都是发出get请求，由于jsonp的形式使用简单，而且关于接收的响应数据，是程序员最多使用的json格式数据，所以该形式在企业中应用比较广泛。

# 动画

在系统操作过程中，用户体验有很多种，系统本身强大的功能体验，服务高效响应的体验，界面优化及视觉效果体验，其中视觉上的动画相关的体验，是用户最直观的体验

系统页面的动画，主要是以多元化的方式展现动态的信息

##
