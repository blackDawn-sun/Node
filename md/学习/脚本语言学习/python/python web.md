#python  #web #flask
## 前置

### 导入包
```python
from flask import Flask
```
### 快速使用
```python
from flask import Flask  
  
app = Flask(__name__)  
  
  
@app.route('/')  
def hello_world():  # put application's code here  
    return 'Hello World!'  
  
  
if __name__ == '__main__':  
    app.run()
```
## 渲染模板文件类似jsp
导入包
```python
from flask import Flask,render_template
```
demo
```python
@app.route('/login')  
def login():  # put application's code here  
    return render_template("login.html")
```
## 重定向
导入包
```python
from flask import Flask, request, make_response
```
demo
```python
@app.route('/') 
def home(): 
	return redirect(url_for('login'))
```
