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


