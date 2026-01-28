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

```