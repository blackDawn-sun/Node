## ajax
### 原生方式
```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>Title</title>  
</head>  
<body>  
  
<button id="send" onclick="toyiyan()">按钮，发送请求</button>  
<span id="result">输出内容</span>  
<script>  
      
    function toyiyan() {  
        // 实例化一个XMLHttpRequest  
        var xhr = new XMLHttpRequest();  
        // 设置回调  readyState状态 有1,2,3,4
        xhr.onreadystatechange = function () {  
            if (xhr.readyState === 4 && xhr.status === 200) {  
                const json = JSON.parse(xhr.responseText);  
                document.getElementById("result").innerText = json["hitokoto"];  
            }  
        }  
        //设置发送请求的方式和请求地址  
        xhr.open("get","https://v1.hitokoto.cn/")  
        //发送请求  
        xhr.send()  
    }  

</script>  
</body>  
</html>
```
post 带请求头和body
```js
var xhr = new XMLHttpRequest();
var url = "你的目标URL";

xhr.open("POST", url, true);

// 设置自定义的header
xhr.setRequestHeader("Content-Type", "application/json"); // 例如，如果你想发送JSON数据
// 如果你需要其他的header，比如认证信息，可以这样设置
// xhr.setRequestHeader("Authorization", "Bearer your_token_here");

xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 请求成功
        console.log(xhr.responseText);
    } else if (xhr.readyState === 4) {
        // 请求失败
        console.error("Error: " + xhr.status);
    }
};

// 要发送的数据，这里以JSON为例
var data = JSON.stringify({ key: "value" });

xhr.send(data);

```
