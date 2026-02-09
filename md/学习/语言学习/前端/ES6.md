## 变量
let -->局部变量
```js
{
	var i = 10
	let j = 11
}
console.log(i) //可以打印出来
console.log(j) //打印不出来

var s = 10
let ss = 12
console.log(window.s) // var声明的全局变量可以变为window对象的属性
console.log(window.ss) //let 声明的不行

const PI = 3.14 //const就说let 的 final修饰的变量
```
## 解构表达式
数组
```js
//数组
let arr = [11,22,33,44,55]
let [a,b,c,d,e=10]=arr //e = 10 是给e默认值
console.log(a,b,c,d,e)
//结果 11 22 33 44 55

```
对象
```js
//对象
let person = {  
    name : "John",  
    age : 20  
}  
let {name, age} = person  
console.log(name,age)
```

## 箭头函数
相当java lamda表达式

```js
let fn1 = function(){}
let fn2 = ()=>{}
let fn3 = x=>{}
let fn4 = x=>console.log(x)
let fn5 = x=>x+1


```
> 箭头函数方法内部的this 指向外层
```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>Title</title>  
</head>  
<body>  
<script>  
  
  
    var win_x = 10  //window 对象的（h5中） win_x  ==> window.win_x
    console.log(this) //win对象  
    let person = {  
        name: '张三',  
        showName:function(){  
            console.log(this) //person 对象  
        },  
        viewName:()=>{  
            console.log(this)  //this  指person 对象 上层 的window对象  
        }  
    }  
    person.showName()  
    person.viewName()  
  
  
  
</script>  
</body>  
</html>
```
