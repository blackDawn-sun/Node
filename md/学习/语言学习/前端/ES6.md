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
## 可变参数
函数入参
```js
function console_arr(a,b,c,... arr) {  
    console.log(a,b,c)  
    console.log(arr)  
}  
  
console_arr(1,2,3,4,5,6)
```
函数调用
```js
function console_arr(a,b,c) {  
    console.log(a,b,c)  
}  
arr = [1,2,3,4,5,6]  
console_arr(... arr)
```
合并数组
```js
let arr1 = [1,2,3]  
let arr2 = [4,5,6]  
let arr3 = [... arr1,... arr2]  
console.log(arr3)
```
合并对象
```js
let person1 = {name: "张三"}  
let person2 = {age: 15}  
let person3 = {sex: "男"}  
let person4 = {...person1, ...person2, ...person3}  
console.log(person4)
```
## 类
```js
class cc{  
    eat(food){  
        console.log(food);  
    }  
  
}  
class Person extends cc{  
    name;  
    age;  
    sex = "男";  
    #name = "10" //私有属性  
    //构造方法  
    constructor(name) {  
        super();  
        this.name = name;  
    }  
    //静态方法  
    static sum(a,b){  
        return a + b;  
    }  
    //set方法  
    set rename(name){  
        console.log("setter");  
        this.#name = name;  
    }  
  
    //get方法  
    get rename(){  
        console.log("getter");  
        return this.#name;  
    }  
}  
let person = new Person();  
person.name = "Jan";  
person.rename= "John2";  
person.age = 12  
console.log(person);  
console.log(person.rename);  
person.eat("水果")
//结果
setter
Person { name: 'Jan', age: 12, sex: '男' }
getter
John2
水果

```
