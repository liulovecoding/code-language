### CSV文件处理
- 用逗号将每个数据分隔开的文件:1,2,4,5,6 //CSV文件的一行内容

```python
import csv
from matplotlib import pyplot as plt      
from datetime import datetime

filename="sitka_weather_2014.csv"
with open(filename) as f:
    reader=csv.reader(f)    #创建阅读文件的阅读器对象
    header_row=next(reader) #从文件第一行读取的一行并换行
    
    #enumerate 获得参数中的每个元素的索引及其值
    for index,column_header in enumerate(header_row):
        print(index,column_header)
```

### JSON文件数据处理

![QQ截图20211124094529](https://user-images.githubusercontent.com/90401274/143156136-925bc1d4-6c71-4ceb-a6ef-0eaf3dae4642.png)

```
import json
import requests

json_url="https://raw.githubusercontent.com/muxuezi/btc/master/btc_close_2017.json"
req=requests.get(json_url)
#通过get方法像GitHub服务器发送请求，将返回结果存储在变量req中

with open("btc_close_2017.json",'w')as f: 
    f.write(req.text)
    #req.text属性直接读取文件数据，返回字符串
file_requests=req.json()
#将JSON文件中的数据转化为列表file_requests
filename='btc_close_2017.json'
with open(filename) as f:
    btc_data=json.load(f)
    #将数据存在字典中

#python 不能直接将待小数点的字符串转化为整形
#需要转换为float or double 在转换为double  
```
### API使用
```
import requests
from requests.models import Response

url='https://api.github.com/search/repositories?q=language:python&sort=stars'   
#这个调用返回GitHub当前托管了多少个Pyhton项目及一些其他信息
#https://api.github.com/：将请求发到Github响应的API调用的部分
#search/repositories：让API搜素Github上的所有仓库
#？表示要传递一个实参，q表示查询，=好让我们指定查询
#language:python&sort=stars 主要语言为python 并将项目按星星数排序

#若GitHub无法全面处理该API，"incomplete_results"的值为true

r=requests.get(url)
print("Status Code:", r.staus_code)
#Status Code的值为200，则请求成功
response_dict=r.json()
print(response_dict.keys())
```
