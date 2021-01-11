# 寫給自己的技術筆記 - 作為程式開發者我們絕對不能忽略的JSON - 教學和用法 - 以JavaScript為例 (一)



## 1. JSON 是什麼?



+ JSON 全名為 JavaScript Object Notation，即 JavaScript 對象標記法
+ 2001年提出
+ 特性: 
    + 輕量型(Light-Weight): 表示產出的檔案非常小
    + 基於文本的(Text-Based): 可以使用文本編譯器(ex. 記事本)開啟
    + 可讀的(Human-Readable)格式: 可以輕鬆被人閱讀
    + 穩定性(Stability): JSON創始人說 JSON 格式永遠不會改變，也就是說很久以前寫的 JSON 文件，很久以後也能使用，就不會有兼容性的問題
+ 和 JavaScript 的關聯
    + JSON名稱中具有 JavaScript，代表它的語法是參考 JavaScript 對象(Object)的，而不是指它只能用於 JavaScript 語言
    + JavaScript 成為網頁上的標準語言，而 JavaScript 的流行，也和 JSON 的流行有著密切相關
    + JSON 是參考JavaScript的語法，所以它的語法與JavaScript定義對象的語法幾乎是完全一樣的
+ JSON 對於人與機器來說都是非常方便閱讀和寫入的，相比於 XML (可延伸標記式語言，Extensible Markup Language)(屬於另一種常見到的數據交換格式)，JSON的文件更小，也讓它快速成為網路上的交換格式





## 2. JSON 的語法規則

+ 格式範例: 

```JSON
{
    "id": 6,
    "name": "Jack",
    "score": [98, 60, 76, 80, 99]
    
    
}
```
+ 講解
    + {}: 對象(object)用大括號表示
    + 變量: name / value 名稱與其對應的值，名稱用雙引號("")包圍，而值可以是字符串、數值、布林值、null、對象(object)和數組(用[]表示)
    + 同層數據之間用逗號(,)隔開




**補充: 可以將寫好的 JSON 放到這個網頁中進行轉換(https://jsoneditoronline.org/#right=local.wepeku)**，它會轉換成更整齊易讀的格式





## 3. JSON VS XML (可延伸標記式語言，Extensible Markup Language)

同樣都是數據交換格式，相較於XML，JSON 所擁有的優勢:

+ 較方便就能使用數組(Array)
+ 並沒有結束標籤(ex. </d>)，整體長度更簡短，讀取與寫入速度更快
+ 可以直接被 JavaScript解析器解析



範例: 

+ JSON
```JSON
{
    "id": 6,
    "name": "Jack",
    "score": [98, 60, 76, 80, 99]
    
    
}

```

+ XML
```XML
<root>
    <id>6</id>
    <name>Jack</name>
    <score>98</score>
    <score>60</score>
    <score>76</score>
    <score>80</score>
    <score>99</score>
</root>
```

這邊就可以很清楚看到XML都需要多加結尾標籤，以及在定義數組上比較麻煩







## 4. JSON 如何解析和生成 (以 JavaScript 為例)



+ JSON.parse(): 將 JSON 格式的字符串，解析為 JavaScript 對象(object)
+ JSON.stringify() 將 JavaScript 對象(object)，轉換成符合 JSON 格式的字符串


```HTML

<script>

// 符合 JSON 格式的字符串
var json_str = '{"id": 6, "name": "Jack", "score": [98, 60, 99]}';

// 轉換成 JavaScript 對象
var js_obj = JSON.parse(json_str);

// 輸出JavaScript對象
console.log("JavaScript Object: ", js_obj)

// 拿 JavaScript 對象轉換成 JSON格式的字符串
var str = JSON.stringify(js_obj)

// 輸出 JSON 格式的字符串
console.log("JSON Format String: ", str)

</script>

```



![image1](images\image1.PNG)





## 5. JSON 格式規定



**重要 :** 大家可以使用線上工具(http://json.cn/)來將自己撰寫的 JSON  文件貼上，它會幫助我們檢查是否有格式錯誤



### 1. 對象 Object:

+ 整個對象用大括號({})包圍起來，裡面由一系列的"名稱: 值"構成
+ 每兩筆並列(同層)的數據之間用逗號(,)分隔，最後一個"名稱: 值"後面不需要加逗號



### 2. 名稱: 值 Name / Vlaue

+ 名稱 name: 為字符串，要用雙引號包起來，切記絕對不能使用單引號或沒有使用任何引號，這方面就和 JavaScript 不同了
+ 值 value: 能選的類型只有七種 - 字符串(string)、數值(number)、對象(object)、數組(array)、布林值(Boolean: True or False)、空值(null)，除了上述其它類型都不符合規定，像是函數(function)、undefined、八進制數(ex. 066)、十六進制數(ex. 0x66)等等



### 3. 字符串 String

+ 一定要用英文的雙括號包起來，不能用單引號或沒有引號
+ 字符串中不能單獨使用一個雙引號("")或是一個右斜槓(\)
+ 如果一定要使用單一雙引號或右斜槓，前面就要多加一個右斜槓，像是\"和\\，當然還有其它的轉義字符也需要這樣





## 6. 解析實作 - 以 JavaScript 為例



+ 解析: 將符合 JSON 語法格式的字符串轉換成指定對象的過程，指定的對象可以是 JavaScript 對象、Python對象、C對象、Java對象等等


### 1. JavaScript 的解析方法

+ JavaScript 的解析方法
    + 第一種: JSON.parse()
    + 第二種: eval()
    + 第三種: 第三方庫，像是JQuery等等


### 2. eval() 方法


+ eval()
    + 函數中的參數為一個字符串，它的作用是直接執行裡面的 JavaScript 程式碼
    + 可以解析 JSON 字符串
    + 很少被使用，除非瀏覽器版本很舊
    + 為一個相對危險的函數，因為直接執行字符串中的程式碼，但字符串中可能含有未知因素導致影響結果
    + **注意: **使用eval()解析符合 JSON 格式的字符串時，要多加一個括號()把字符串包住，不然會報錯，因為eval()會把它當成程式碼區塊(語句)來執行，所以要在兩旁加上括號，讓它成為表達式





範例一: 使用eval()解析JavaScript字符串

```HTML
<script>

// 將 JavaScript 程式碼包成字符串
var js_str = "console.log('Hi Hi')";

// 使用eval()來解析這個字符串
eval(js_str)

</script>
```

![image2](images\image2.PNG)



範例二: 使用eval()解析符合JSON格式字符串，並轉換成JavaScript對象

+ **注意: **使用eval解析符合JSON格式字符串時，要多加一個括號()把字符串包住，不然會報錯，因為eval()會把它當成程式碼區塊(語句)來執行，所以要在兩旁加上括號，讓它成為表達式

```HTML
<script type = "text/javascript">

// 符合JSON格式的字符串
var str = '{"name": "Jack", "score": 99}';

// 轉成JavaScript對象
var js_object = eval("(" + str + ")");

// 印出
console.log(js_object)

</script>
```



![image3](images\image3.PNG)

### 3. JSON.parse() 方法



最常使用的方法

範例一:

```HTML
<script type = "text/javascript">

// 符合JSON格式的字符串
var str = '{"name": "Jack", "score": 99}';

// 轉成JavaScript對象
var js_object = JSON.parse(str);

// 印出
console.log(js_object);

</script>

```

![image4](images\image4.PNG)



**進階應用**

+ JSON.parse() 擁有兩個參數，第一個為我們欲轉換的JSON格式字符串，第二個為一個函數，此函數中有兩個參數: name 和 value
+ 當於 JSON.parse()中傳入符合 JSON 格式的字符串後，JSON 中的每一組名稱:值(name:value)都會執行(調用)該函數
+ 該函數會有返回值，返回值會直接賦值給對應的名稱(name)
+ 使用這個方法，可以在解析符合 JSON 格式字符串的同時，進行一些我們自定義的數據處理



範例二: 

```HTML
<script type = "text/javascript">

// 符合JSON格式的字符串
var str = '{"name": "Jack", "score": 99, "class": "A"}';

// 自定義的函數
function process(name, value) {
    console.log(name + "=" + value);
    return value
};


// 轉成JavaScript對象
var js_object = JSON.parse(str, process);

// 印出
console.log(js_object);

</script>
```



![image5](images\image5.PNG)





**結果講解:**

= [object Object]: 表示的是整個{"name": "Jack", "score": 99, "class": "A"}'對象，然後它的值(value)為對象本身，而因為它沒有名稱，所以=前面為空



範例三: 當我想要把名稱為score的都加1

```HTML
<script type = "text/javascript">

// 符合JSON格式的字符串
var str = '{"name": "Jack", "score": 99, "class": "A"}';

// 自定義的函數
function process(name, value) {


    if(name == 'score'){
        value += 1;
    }
    return value;
};


// 轉成JavaScript對象
var js_object = JSON.parse(str, process);

// 印出
console.log(js_object);

</script>
```





## 7. 序列化和反序列化處理過程

+ Marshalling / Encoder 序列化: 代表將 JavaScript 的值轉換為 JSON 字符串，使用方法 - JSON.stringify()
+ Unmarshalling / Decoder 反序列化: 代表將 JSON 字符串轉換為 JavaScript 值，使用方法 - JSON.parse





## 8. 序列化方法 - JSON.stringify



### 1. JSON.stringify() 參數介紹

```JavaScript
JSON.stringify(value [, replacer[, space]])
```

+ value: 一定要有的參數，要轉換的 JavaScript 值，一般狀況下為對象(Object)或數組(Array)
+ replacer: 可以忽略不用的參數，它有兩種帶入方式: 函數或是數組
    + 函數: 每一組名稱: 值(name:value)都會執行(調用)這個函數，會返回一個值，作為名稱(name)的對應值(value)，並轉換進結果的字符串裡面
    + 數組: 規定只有數組中有的名稱(name)才能夠轉換，而且轉換後的順序與數組中的順序會是一樣的
+ space: 可以忽略不寫，是為了更好閱讀而存在，能夠在 JSON 字符串中添加空白或制表符等等



### 2. value 參數用法



範例一: 

```HTML
<script type = "text/javascript">

// 定義 JavaScript 對象

var js_obj = {
    name: "Jack",
    score: "99"


};

console.log("JavaScript Object: ", js_obj);

// 轉換為 JSON 字串
var json_str = JSON.stringify(js_obj);

console.log("JSON Format: ", json_str)


</script>
```



![image6](images\image6.PNG)

範例二: 不符合規則的情況，基本上會被省略

```HTML
<script type = "text/javascript">

// 定義 JavaScript 對象

var js_obj = {

    // 符合語法規則
    name: "Jack",
    score: "99",

    // 不符合語法規則，轉換過程中會被省略
    class: undefined,
    run: function r(){
    },

    // 不符合語法規則，轉換過程中數組內部會被返回null空值
    jump: [function() {}]

};

console.log("JavaScript Object: ", js_obj);

// 轉換為 JSON 字串
var json_str = JSON.stringify(js_obj);

console.log("JSON Format: ", json_str)


</script>
```

![image7](images\image7.PNG)



### 3. replacer 參數用法

+ 為函數的狀況:



範例一: 將名稱為"score"的值增加1

```HTML
<script type = "text/javascript">

// 定義 JavaScript 對象

var js_obj = {
    name: "Jack",
    score: "99"


};

console.log("JavaScript Object: ", js_obj);


// 自行定義函數，將名稱為"score"的值加1

function add_score(name, value){
    if (name == 'score'){
        value += 1

        
       };
    return value

};




// 轉換為 JSON 字串
var json_str = JSON.stringify(js_obj);

console.log("JSON Format: ", json_str)


</script>
```

![image8](images\image8.PNG)




+ 為數組的情況


```HTML
<script type = "text/javascript">

// 定義 JavaScript 對象

var js_obj = {
    'Jack': 99,
    'Ann': 90,
    'Ken': 86,
    'Jen': 75
};

console.log("JavaScript Object: ", js_obj);

// 轉換為 JSON 字串
var json_str = JSON.stringify(js_obj, ["Jack", "Jen", "Ann"]);

console.log("JSON Format: ", json_str)


</script>
```

![image9](images\image9.PNG)





### 4. space 參數用法



範例一: 多加一個space參數，寫入"Student"

```HTML
<script type = "text/javascript">

// 定義 JavaScript 對象

var js_obj = {
    'Jack': 99,
    'Ann': 90,
    'Ken': 86,
    'Jen': 75
};

console.log("JavaScript Object: ", js_obj);

// 轉換為 JSON 字串
var json_str = JSON.stringify(js_obj, ["Jack", "Jen", "Ann"], "Student");

console.log("JSON Format: ", json_str)


</script>
```



![image10](images\image10.PNG)



範例二: 添加制表符(ex. \t、\n、\r等等)

```HTML
<script type = "text/javascript">

// 定義 JavaScript 對象

var js_obj = {
    'Jack': 99,
    'Ann': 90,
    'Ken': 86,
    'Jen': 75
};

console.log("JavaScript Object: ", js_obj);

// 轉換為 JSON 字串
var json_str = JSON.stringify(js_obj, ["Jack", "Jen", "Ann"], "\n");

console.log("JSON Format: ", json_str)


</script>
```



![image11](images\image11.PNG)



