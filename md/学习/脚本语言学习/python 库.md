#python 
# 内置库

## time
导入
```python
import time
```
功能：
sleep
```python
time.sleep(1)
```
## subprocess
导入
```python
import subprocess
```
功能实例：
检测端口占用功能
```python

def check_port_via_cmd(port):  
    """  
    使用 netstat 命令检查端口  
    """    # -a 显示所有连接，-n 以数字形式显示，-o 显示 PID    cmd = f"netstat -ano | findstr :{port}"  
    result = subprocess.run(cmd, shell=True, capture_output=True, text=True)  
  
    # 如果输出中包含 "LISTENING" 或有内容输出，通常表示被占用  
    if result.stdout and "LISTENING" in result.stdout:  
        return True, result.stdout  
    else:  
        return 0
```
## os
导入
```python
import os
```
功能：
```python
os.getpid() #当前进程 pid
os.getppid() #父进程 pid
os.mkdir() #创建文件夹
os.getcwd() #当前项目绝对路径
```
## os.path
导入
```python
import os.path
```
功能：
```python
os.path.exists(file_path)
```
## multiprocessing
导入
```python
from multiprocessing import Process,Lock,RLock
```
功能：
加锁：
```python
import os  
from multiprocessing import Process,Lock,RLock  
  
  
  
def process1(lock):  
    num = 100  
    for i in range(1,num+1):  
        lock.acquire() #上锁，Rlock会记录层数，lock锁二次上锁会变成死锁  
        lock.acquire()  
        print(f"我是process1 进程,正在执行第 {i} 件事情:")  
        lock.release()  
        print(f"当前进程是 {os.getpid()}, 父进程是 {os.getppid()}")  
        lock.release() #释放锁  
  
def process2(lock,n,j):  
    num = 100  
    for i in range(1,num+1):  
        with lock: #自动释放锁  
            print(f"我是process2 进程,正在执行第 {i} 件事情 n:{n} j:{j}")  
            print(f"当前进程是 {os.getpid()}, 父进程是 {os.getppid()}")  
  
if __name__ == "__main__":  
    print(f"开始创建进程,主进程是 {os.getpid()}")  
    # lock = Lock()  
    lock = RLock()  
    p1 = Process(target=process1,args=(lock,))  
    p2 = Process(target=process2,args=(lock,20,30))  
  
    p1.start()  
    p2.start()  
    print("结束运行")
```
## json
导入
```python
import json
```
功能：
```python
payload = {  
    "jsonrpc": "2.0",  
    "id": "1",  
    "method": "aria2.addUri"
}
data=json.dumps(payload)
```


# 第三方库
修改第三方

## pandas
安装库
```python
pip install pandas # 使用pip安装
```
导入
```python
import pandas as pd
from openpyxl.styles import Alignment, Font #表格美化
```
功能：
表格写入 和合并单元格
```python
def write_to_excel(data, parent_file=WsVideo.down_path):  
    # 将数据转换为DataFrame  
  
    data = [d.__dict__ for d in data]  
  
    # 自定义表头和列的顺序  
    custom_columns = ['video_week', 'video_day', 'video_name', 'video_rename', 'video_url']  
    # 将数据转换为DataFrame  
    df = pd.DataFrame(data)  
    # 选择并重新排列列的顺序  
    df = df[custom_columns]  
    # 自定义表头  
    df.columns = ['周数', '日期', '系统内视频标题名', '视频文件名', '视频地址']  
  
    if not os.path.exists(parent_file):  
        os.mkdir(parent_file)  
    # 定义输出文件名  
    output_file = parent_file + '/大纲.xlsx'  
  
    # 将DataFrame写入Excel文件（先不保存）  
    with pd.ExcelWriter(output_file, engine='openpyxl') as writer:  
        df.to_excel(writer, sheet_name='Sheet1', index=False)  
        # 加载工作簿和活动工作表  
        # workbook = writer.book  
        worksheet = writer.sheets['Sheet1']  
        # 获取最大行数和列数  
        max_row = worksheet.max_row  
        max_col = worksheet.max_column  
        # 遍历每一列，合并相同数据的单元格  
        for col in range(1, max_col + 1):  
            last_value = None  
            start_row = 2  # 从第二行开始，跳过标题行  
  
            for row in range(2, max_row + 1):  
                current_cell = worksheet.cell(row=row, column=col)  
  
                # 单独处理最后一行的合并  
                if max_row == row and current_cell.value == last_value:  
                    end_row = row  
                    worksheet.merge_cells(start_row=start_row, start_column=col, end_row=end_row, end_column=col)  
  
                if current_cell.value == last_value:  
                    continue  
                else:  
                    if last_value is not None:  
                        end_row = row - 1  
                        if start_row != end_row:  
                            worksheet.merge_cells(start_row=start_row, start_column=col, end_row=end_row,  
                                                  end_column=col)  
  
                    last_value = current_cell.value  
                    start_row = row  
  
        # 处理最后一组相同的值  
        if start_row != max_row:  
            worksheet.merge_cells(start_row=start_row, start_column=col, end_row=max_row, end_column=col)  
  
        # 调整字体和对齐方式（可选）  
        for row in worksheet.iter_rows(min_row=1, max_row=1, min_col=1, max_col=max_col):  
            for cell in row:  
                cell.font = Font(bold=True)  
                cell.alignment = Alignment(horizontal='center')  
  
    print(f"数据已成功写入 {output_file} 并合并了相同数据的单元格")
```
表格读取
```python
def read_excel(path= WsVideo.down_path):  
    file_path = path + "/大纲.xlsx"  
    print(f"准备读取大纲文件，地址: {file_path}")  
  
    if not  os.path.exists(file_path):  
        print(f"不存在大纲文件，地址：{file_path}")  
        return []  
    df = pd.read_excel(file_path)  
    # 处理合并单元格导致的空值  
    # df_clean = df.fillna(method='ffill')  
    df_clean = df.ffill()  
  
    # 将数据转换为字典列表 (每行一个字典)  
  
    data_list = df_clean.to_dict(orient='records')  
    print(f"读取大纲文件成功：dict:{data_list}")  
    return data_list
```
## requests
安装库
```python
pip install requests
```
导入
```python
import requests
```
功能：
发送请求
```python
def request_week_info(token):  
    header = {  
        "authorization": "Bearer " + token,  
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/144.0.0.0 Safari/537.36"  
    }  
  
    url = "http://cg.wangshijiaoyujituan.cn/prod-api/home/teacherHomework/selectClassWeekInfoByClassId?classId=1683"  
    rsp = requests.get(url, headers=header)  
    rsp.raise_for_status()  #非200返回报错
    print(rsp.json())  
    return rsp.json()
```

