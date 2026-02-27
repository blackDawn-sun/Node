#vue 
## 导入vue3
### 远程文件导入
```js
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```
### 本地文件导入
![](assets/vue3/file-20260227141329273.js)
## Vue非工程化使用
```html
<!doctype html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1">  
    <title>Document</title>  
<!--    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>-->  
    <script src="./vue.js"></script>  
</head>  
<body>  
  
<div id="app">  
    <h1>{{title}}</h1>  
    <h1 v-text="message" v-bind:style="colorStyle">你好</h1>  
    <button @click="fun1()"> 按钮 </button>  
</div>  
  
<script>  
    const app = Vue.createApp({  
        setup(){  
            let message = 'hello world'  
            let title = 'Hello World title'  
            let colorStyle = {"background-color":"yellow"};  
            let fun1 = function() {  
                alert("Hello World!")  
            }  
            // return 返回的变量和方法才能和HTML元素关联  
            return {  
                message,title,colorStyle,fun1  
            }  
        }  
    })  
    //将app对象挂载在指定的元素上，被挂载的元素内部就可以通过vue框架实现数据的渲染了  
    app.mount("#app")  
  
</script>  
  
</body>  
</html>
```
## Vue工程化
### 安装vite
```
npm create vite@latest 
Need to install the following packages:
create-vite@8.3.0
Ok to proceed? (y) y //第一次会出现，下载vite
```
## vue语法
### 文本渲染
v-text
```vue
<span v-text="ref_count"></span>
```
v-html
### 属性渲染
v-bind:属性=“”
简写： :属性

```vue
<script setup>
	const data= {  
	  logo: "http://www.atguigu.com/images/index_new/logo.png",  
	  name: "尚硅谷",  
	  url: "http://www.atguigu.com"  
	}
</script>
<template>
	<a v-bind:href="data.url">  
	  <img v-bind:src="data.logo" v-bind:title="data.name">  
	  <img :src="data.logo" :title="data.name">  简写
	</a>
</template>
<style scoped>  
  
</style>
```
### 事件渲染
v-on:事件名称 = “函数名”
v-on:事件名 可以简写  @事件名
原生的js事件 on*** onclick ondbclick onblur
```vue
<script setup>
	function fun1() {  
	  alert("hi")  
	}  
	let a = ref(1)  //双向绑定
	function fun2() {  
	  a.value++  
	}  
	function fun3(event) {  
	  let flag = confirm("确定要访问目标链接吗")  
	  if (!flag) {// 原生js编码方式阻止组件的默认行为  
	    event.preventDefault()  
	  }  
	}  
	function fun4() {  
	  alert("超链接被点击了")  
	}
</script>
<template>
	<!--事件的绑定函数 -->  
	<button v-on:click="fun1()">hello</button>  
	<button v-on:click="fun2()">+</button>  
	<!--内联事件处理器-->  
	<button v-on:click="a++">+</button>  
	<!--事件的修饰符.once事件只绑定一次 prevent 修饰符阻止组件的默认行为 -->  
	<button v-on:click.once="a++">+</button>  
	{{ a }}  
	<br>  
	<a href="http://www.atguigu.com" v-on:click="fun3($event)">尚硅谷</a>  
	<a href="http://www.atguigu.com" v-on:click.prevent="fun4()">尚硅</a>
</template>
<style scoped>  
  
</style>
```
### 响应式数据
#### ref 
适合单个变量
script 中使用 需要带.value  
template中使用不需要.value
```vue
<script setup>
	import {ref} from 'vue';
	let a = ref(1)  //双向绑定
	function fun1() {  
	  a.value++  
	}  
	
</script>
<template>
	<button v-on:click="fun1()">+</button>  
	{{ a }}  
</template>
<style scoped>  
  
</style>
```
#### reactive 
适合对象
reactive(对象)  
```vue
<script setup>
	import {reactive} from 'vue';
	let person = {  
	  age: 10,  
	  name: "小米",  
	  sex: "男"  
	}  
	let person_reactive = reactive(person)  
	function agg_add(){  
	  person_reactive.age++  
	}
</script>
<template>
	<button @click="agg_add()">age +</button>  
	{{person_reactive.age}}
</template>

<style scoped>  
  
</style>
```
#### toRef
将对象里的数据转成响应式数据
```vue
<script setup>
	import {toRefs} from 'vue';
	
	
</script>
<template>

</template>
<style scoped>  
  
</style>
```