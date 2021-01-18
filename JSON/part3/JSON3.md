# 寫給自己的技術筆記 - 作為程式開發者我們絕對不能忽略的JSON - Python 如何處理JSON文件





哈囉，由於JSON系列的第一篇(寫給自己的技術筆記 - 作為程式開發者我們絕對不能忽略的JSON - 教學和用法 - 以JavaScript為例(一))已經針對JSON做過介紹了，所以這篇就不會再詳細介紹JSON囉，這篇會把重點放在如何使用Python來處理JSON檔案





## 1. JSON 介紹

+ JSON 全名為 JavaScript Object Notation，即 JavaScript 對象標記法
+ 2001年提出
+ 特性: 
    + 輕量型(Light-Weight): 表示產出的檔案非常小
    + 基於文本的(Text-Based): 可以使用文本編譯器(ex. 記事本)開啟
    + 可讀的(Human-Readable)格式: 可以輕鬆被人閱讀
    + 穩定性(Stability): JSON創始人說 JSON 格式永遠不會改變，也就是說很久以前寫的 JSON 文件，很久以後也能使用，就不會有兼容性的問題
+ 目前 REST API 的主流形式，可見它在數據交換格式的重要性







## 2. Python中的JSON套件

+ json套件: Python中用來編碼和解碼JSON文件的套件
+ json套件為Python中自帶的套件，所以不用額外安裝，只需要直接載入即可



### JSON 和 Python 資料型態轉換表

#### Python 轉 JSON

|Python|JSON|
|---|---|
|dict|object|
|list, tuple|array|
|str, unicode|string|
|int, long, float|number|
|True|true|
|False|false|
|None|none|



#### JSON 轉 Python

|JSON|Python|
|---|---|
|object|dict|
|array|list|
|string|unicode|
|number(int)|long, int|
|number(real)|float|
|true|True|
|false|False|
|null|None|





## 3. Python 如何處理 JSON 套件

**處理過程分成:**

+ Marshalling / Encoder 序列化: 代表將 Python 的物件資料轉換成為 JSON 物件，使用方法 - json.dumps 或 json.dump
+ Unmarshalling / Decoder 反序列化: 代表將 JSON 物件轉換成為 Python 的資料物件，使用方法 - json.loads 或 json.load



**使用方法**

|函數|說明|
|---|---|
|json.dumps|將Python對象(Object)編碼成JSON格式的字符串|
|json.dump|將Python字典轉成JSON後，寫入JSON文件|
|json.loads|將JSON字符串解碼成為Python對象(Object)|
|json.load|直接讀取JSON文件，並轉成Python字典|



**完整參數**

+ json.dumps

```
dumps(obj, *, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)
```

+ json.dump

```
dump(obj, fp, *, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)
```

+ json.loads

```
loads(s, *, encoding=None, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)
```

+ json.load

```
load(fp, *, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)
```





## 4. 實作







### JSON 檔案或字符串 轉 Python字典



#### 1. 從JSON檔中導入

+ 我們有一份JSON擋 - test.json

```JSON
{
    "Student 1": {
        "Student_id": 126,
        "Name": "Jack",
        "Score": 99,
        "Friends": ["Tim", "Jen", "Ken"]
    },

    "Student 2": {
        "Student_id": 128,
        "Name": "Ken",
        "Score": 99,
        "Friends": ["Jack", "Jessy", "Cathy"]
    }
}

```






+ 方法一: json.load

```Python
import json

## 讀取JSON檔
with open('test.json', 'r') as f:
    ## 轉成Python Dict
    python_dict = json.load(fp = f)
    
print("Python Dict: ", python_dict)
print("Type: ", type(python_dict))
```



```
Python Dict:  {'Student 1': {'Student_id': 126, 'Name': 'Jack', 'Score': 99, 'Friends': ['Tim', 'Jen', 'Ken']}, 'Student 2': {'Student_id': 128, 'Name': 'Ken', 'Score': 99, 'Friends': ['Jack', 'Jessy', 'Cathy']}}
Type:  <class 'dict'>
```







+ 方法二: json.loads

```Python

import json

## 讀取JSON檔
with open('test.json', 'r') as f:
    ## 將內容裝進text
    text = f.read()
    
print("JSON Format: ", text)
print("Type: ", type(text))
print("From JSON String Transform To Python Dict")
print("Python Dict: ", json.loads(text))
print("Type: ", type(json.loads(text)))



```

```
JSON Format:  {
    "Student 1": {
        "Student_id": 126,
        "Name": "Jack",
        "Score": 99,
        "Friends": ["Tim", "Jen", "Ken"]
    },

    "Student 2": {
        "Student_id": 128,
        "Name": "Ken",
        "Score": 99,
        "Friends": ["Jack", "Jessy", "Cathy"]
    }
}

Type:  <class 'str'>
From JSON String Transform To Python Dict
Python Dict:  {'Student 1': {'Student_id': 126, 'Name': 'Jack', 'Score': 99, 'Friends': ['Tim', 'Jen', 'Ken']}, 'Student 2': {'Student_id': 128, 'Name': 'Ken', 'Score': 99, 'Friends': ['Jack', 'Jessy', 'Cathy']}}
Type:  <class 'dict'>
```



#### 2. 有一筆JSON Format的字符串 轉 Python Dict

+ 只能使用json.loads

```Python
import json

## JSON Format的字符串
text = '{"Name":"Jack", "Score": 99}'

print("JSON Format: ", text)
print("Type:, "type(text))
print("From JSON String Transform To Python Dict")
print("Python Dict: ", json.loads(text))
print("Type: ", type(json.loads(text)))

```

```
JSON Format:  {"Name":"Jack", "Score": 99}
Type: <class 'str'>
From JSON String Transform To Python Dict
Python Dict:  {'Name': 'Jack', 'Score': 99}
Type:  <class 'dict'>
```



### Python 字典(Dict) 轉 JSON字符串



#### 1. 寫入到JSON檔 - 會自動保存成JSON檔



+ 方法一: json.dump

```Python
import json

## Python 字典
python_dict = {
    'Name': "Jack",
    'Score': 99
}

## 存成JSON File
with open("python2json.json", 'w') as f:
    json.dump(python_dict, f)  
```

![image1](images\image1.PNG)

+ 方法二: json.dumps

```Python
import json

## Python 字典
python_dict = {
    'Name': "Jack",
    "Score": 99,
}
print("Python Dict: ", python_dict)
print("Type: ", type(python_dict))
print("From Python Dict Transform To JSON Format")
print("JSON Format: ", json.dumps(python_dict))
print("Type: ", type(json.dumps(python_dict)))

## 存成JSON File
with open('python2json1.json', 'w') as f:
    f.write(json.dumps(python_dict))
```

```
Python Dict:  {'Name': 'Jack', 'Score': 99}
Type:  <class 'dict'>
From Python Dict Transform To JSON Format
JSON Format:  {"Name": "Jack", "Score": 99}
Type:  <class 'str'>
```

![image2](images\image2.PNG)







#### 2. 轉成 JSON Format的字符串

+ 只能使用函數: json.dumps
```Python
import json

## Python 字典
python_dict = {
    'Name': "Jack",
    "Score": 99,
}
print("Python Dict: ", python_dict)
print("Type: ", type(python_dict))
print("From Python Dict Transform To JSON Format")
print("JSON Format: ", json.dumps(python_dict))
print("Type: ", type(json.dumps(python_dict)))
```
```
Python Dict:  {'Name': 'Jack', 'Score': 99}
Type:  <class 'dict'>
From Python Dict Transform To JSON Format
JSON Format:  {"Name": "Jack", "Score": 99}
Type:  <class 'str'>
```







### Python 字典(Dict)中包含list 轉 JSON 字符串

+ 範例: 這邊是使用dumps來存進檔案
```Python
import json

## Python 字典
python_dict = {
    "Student A": {
        "Student_id": 126,
        "Name": "Jack",
        "Score": 99,
        "Friends": ["Tim", "Jen", "Cindy"]
    },
    
    "Student B":{
        "Student_id": 128,
        "Name": "Ken",
        "Score": 98,
        "Friends": ["Jack", "Jessy", "Cathy"]
    }
}
print("Python Dict: ", python_dict)
print("Type: ", type(python_dict))
print("From Python Dict Transform To JSON Format")
print("JSON Format: ", json.dumps(python_dict))
print("Type: ", type(json.dumps(python_dict)))

## 存成JSON File
with open('python2json2.json', 'w') as f:
    f.write(json.dumps(python_dict))
```

```
Python Dict:  {'Student A': {'Student_id': 126, 'Name': 'Jack', 'Score': 99, 'Friends': ['Tim', 'Jen', 'Cindy']}, 'Student B': {'Student_id': 128, 'Name': 'Ken', 'Score': 98, 'Friends': ['Jack', 'Jessy', 'Cathy']}}
Type:  <class 'dict'>
From Python Dict Transform To JSON Format
JSON Format:  {"Student A": {"Student_id": 126, "Name": "Jack", "Score": 99, "Friends": ["Tim", "Jen", "Cindy"]}, "Student B": {"Student_id": 128, "Name": "Ken", "Score": 98, "Friends": ["Jack", "Jessy", "Cathy"]}}
Type:  <class 'str'>
```

![image3](images\image3.PNG)





大家也可以試試用json.dump的方式存成JSON檔喔





## 5. 重要補充: 如果寫進JSON檔，想要更易讀的格式來寫



+ 前面的範例中，當我們把Python Dict轉成JSON Format的字符串時，都會變成一排(行)，但實際上的狀況是我們需要閱讀這些JSON檔，如果數據一多就會很難閱讀


+ 在json.dumps()裡面填上一個參數indent，用來指定每行開頭要空幾格




+ 範例一: 我將indent設4，代表空四格

```Python
import json

## Python 字典
python_dict = {
    'Name': "Jack",
    "Score": 99,
}
print("Python Dict: ", python_dict)
print("Type: ", type(python_dict))
print("From Python Dict Transform To JSON Format")
print("JSON Format: ", json.dumps(python_dict))
print("Type: ", type(json.dumps(python_dict)))

## 存成JSON File
with open('python2json3.json', 'w') as f:
    f.write(json.dumps(python_dict, indent = 4))
```

```
Python Dict:  {'Name': 'Jack', 'Score': 99}
Type:  <class 'dict'>
From Python Dict Transform To JSON Format
JSON Format:  {"Name": "Jack", "Score": 99}
Type:  <class 'str'>
```

![image4](images\image4.PNG)



+ json.dump也擁有參數indent喔



+ 範例二:


```Python
import json

## Python 字典
python_dict = {
    "Student A": {
        "Student_id": 126,
        "Name": "Jack",
        "Score": 99,
        "Friends": ["Tim", "Jen", "Cindy"]
    },
    
    "Student B":{
        "Student_id": 128,
        "Name": "Ken",
        "Score": 98,
        "Friends": ["Jack", "Jessy", "Cathy"]
    }
}
print("Python Dict: ", python_dict)
print("Type: ", type(python_dict))
print("From Python Dict Transform To JSON Format")
print("JSON Format: ", json.dumps(python_dict))
print("Type: ", type(json.dumps(python_dict)))

## 存成JSON File
with open('python2json4.json', 'w') as f:
    f.write(json.dumps(python_dict, indent = 4))
    f.write('\n')
```



```
Python Dict:  {'Student A': {'Student_id': 126, 'Name': 'Jack', 'Score': 99, 'Friends': ['Tim', 'Jen', 'Cindy']}, 'Student B': {'Student_id': 128, 'Name': 'Ken', 'Score': 98, 'Friends': ['Jack', 'Jessy', 'Cathy']}}
Type:  <class 'dict'>
From Python Dict Transform To JSON Format
JSON Format:  {"Student A": {"Student_id": 126, "Name": "Jack", "Score": 99, "Friends": ["Tim", "Jen", "Cindy"]}, "Student B": {"Student_id": 128, "Name": "Ken", "Score": 98, "Friends": ["Jack", "Jessy", "Cathy"]}}
Type:  <class 'str'>
```





![image5](images\image5.PNG)

















