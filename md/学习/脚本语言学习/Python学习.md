#python 

## 关键字
![](assets/Python学习/file-20260128105044141.png)
## 变量
```python
age = 10
```
常量(约定，使用全大写表示常量)
```python
AGE = 10
```
## 注释
单行注释： #
多行注释： 三个引号
```python
"""
多行注释 也是字符串，无变量使用解释器会员忽略
"""
'''
这个也是多行注释
'''

#单行注释

```
## 数据类型
![](assets/Python学习/file-20260128110041120.png)
- type() 函数可以查数据类型
```python
print(type("你好"))
#返回： <class 'str'>
```
- 整数
可以三位一组用下划线隔开
```python
xx = 10_000_00  
print(xx)
```
- 浮点数
![](assets/Python学习/file-20260128110744918.png)
- 字符串
![](assets/Python学习/file-20260128111325982.png)
 %s %d %f
![](assets/Python学习/file-20260128111605770.png)
![](assets/Python学习/file-20260128111635367.png)
![](assets/Python学习/file-20260128111721601.png)
- 数据类型转换
```python
print(type(str(1_000)))  
print(int(56.123))  
print(float(120))  
print(bool(0)) #布尔类型
#返回
<class 'str'>
56
120.0
False
```
## 运算符
![500](assets/Python学习/file-20260128112401003.png)

![500](assets/Python学习/file-20260128112522600.png)
![500](assets/Python学习/file-20260128114847745.png)
![500](assets/Python学习/file-20260128115214373.png)
![](assets/Python学习/file-20260128115456151.png)
or同理
not 返回一定是布尔值

## 常用函数
### input()
![](assets/Python学习/file-20260128120131083.png)
### 字符串函数
string.split(string) 分割返回为列表
string.strip(string) 去除首尾包含的字符字符
len(string) 长度
max(string) 返回unicode编码最大的字符
min(string) 返回unicode编码最小的字符
sort(string) unicode编码排序后返回


## 流程判断
### 判断
if-elif-else
```python
num = int(input("班上有多少人: "))  
if if 0 < num < 10::  # 相当 num>0 and num<10 简写
    print("小班")  #4个空格的缩进
elif 20 > num > 10:  # 相当 num<20 and num >10 简写
    print("中班")  #4个空格的缩进
else:  
    print(f"既不是小班也不是中班，班级人数去掉老师是{num-1}人,你自己看吧")
```
### 循环
while
```python
n = 1  
while n<10:  
    n+=1  
    print(f"n= {n}")  
print(f"end while , n= {n}")
```
for
> 可以使用 continue  , break

```python
#使用range
for n in range(1,5): #range 左闭右开[1,5) 相当于[1,2,3,4]  
    print(f"n = {n}")  
print("end for ")

#字符串也可用for
for n in "abcdee": #相当于[a,b,c,d,e,e]  
    print(f"n = {n}")  
print("end for ")
```
## 函数

```python
def sumAges(name, needAddAge, age, sex="男",*agrs):  #可变参数(*agrs)相当java ...
    if age < 20:  
  
        print(f"姓名{name},年龄小于20，加年龄{needAddAge}，性别是{sex}")  
        print(agrs)  
        return needAddAge + age  
    elif age > 100:  
        print(f"姓名{name},年龄大于20，不真实，返回none，性别是{sex}")  
        return None  
    else:  
        print(f"姓名{name},年龄在20-100，成年人，不加年龄，性别是{sex}")  
        return age  
  
print(sumAges("张三",1,10,"NI","Hao","python"))  
print(sumAges("老李", 1, 20, sex="女"))  
print(sumAges("老了", 2, 1000,"男","NI","Hao","python"))
```

## 作用域
局部作用域 需要 改变全局作用域的值是，需要声明改的是全局作用域
```python
s = 100  
def printa2b():  
    global s  
    s = 200  
    print(s)  
printa2b()  
print(s)
```

## 数据容器
> 存放一个个元素的地方

### 常用方法
![](assets/Python学习/file-20260128132521222.png)
![](assets/Python学习/file-20260128133345973.png)
#### sum()
in
not in 
count(item) 计数
### 列表（list）
类似 list集合 和数组
格式： [a,b,c,[aa,bb,cc],d] 
有下标，从0开始 
```python
list = ["a","b",["aa","bb"],"c"]  
print(list[2][1])
```
#### 操作方法
##### 增
![](assets/Python学习/file-20260128131822850.png)
##### 删
![](assets/Python学习/file-20260128132001154.png)
##### 改
a[0] = 1
##### 查
a[0]
#### 常用方法
![](assets/Python学习/file-20260128132350847.png)
#### 转换
![](assets/Python学习/file-20260128143234664.png)
### 元祖
> 元祖数据不可修改 
> 格式 （a,b,c）

![](assets/Python学习/file-20260128133117753.png)
#### 转换
![](assets/Python学习/file-20260128143316314.png)
### string
#### 转换
![](assets/Python学习/file-20260128143459676.png)

### 序列
列表，元祖，string 都是序列
切片 就是取序列里的一部分元素
```python
# [起始元素，结束元素，步长] 左闭右开 可省略写 如list[:99:] list[1::] list[::1]
list = [1,2,3,4,5,6,7,8,9]  
print(list[2:8:2])
#返回 [3, 5, 7]
```
相加
```python 
list = [1,2,3]  
list2 = [4,5,6,7,8,9]
list3 = list + list2
#返回 [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
相乘（重复添加）
```python
list = [1,2,3]    
list3 = list * 2  
print(list3)
#返回 [1, 2, 3, 1, 2, 3]
```

### 集合
无序，去重
格式： {}
frozenset 是不可变的
```python
set = frozenset("strings")  
print(set)
```
空集合
```python
a = set()
```
![](assets/Python学习/file-20260128141031173.png)
#### 操作方法
![](assets/Python学习/file-20260128141151718.png)
![](assets/Python学习/file-20260128141259237.png)
#### 常用方法
![](assets/Python学习/file-20260128141435934.png)
![](assets/Python学习/file-20260128141451245.png)
![](assets/Python学习/file-20260128141515892.png)
![](assets/Python学习/file-20260128141532030.png)
![](assets/Python学习/file-20260128141550761.png)
![](assets/Python学习/file-20260128141718167.png)
#### 转换
![](assets/Python学习/file-20260128143401089.png)
#### 简写
![](assets/Python学习/file-20260128144108483.png)
### 字典
类似map ,key有去重能力
key 不可变类型，可以是序列和集合 ,value 任意类型
格式：{key:value,key,value}
#### 操作方法
![](assets/Python学习/file-20260128142551691.png)
#### 常用方法
![](assets/Python学习/file-20260128142834611.png)
#### 字典遍历
![](assets/Python学习/file-20260128142934166.png)
#### 转换
![](assets/Python学习/file-20260128143647640.png)
### 面向对象
#### 创建对象
![](assets/Python学习/file-20260128144655953.png)
#### 实例化对象
![](assets/Python学习/file-20260128144926680.png)
#### 获取和修改对象
![](assets/Python学习/file-20260128145042660.png)
#### 创建方法
![](assets/Python学习/file-20260128145354981.png)
