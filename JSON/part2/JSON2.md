# 寫給自己的技術筆記 - 作為程式開發者我們絕對不能忽略的JSON - JSON和XML間如何互相轉換 - GeoJSON & TopoJSON地理資訊教學 - 以JavaScript為例(二)





## 1. 如何讓檔案在 JSON 和 XML 間互相轉換?



### STEP 1: 安裝相關文件

+ JQuery - https://jquery.com/download/
+ jquery.json2xml.j - https://www.json110.com/component.html
+ jquery.xml2json.js - https://www.json110.com/component.html





![download](images\download.PNG)



### STEP 2: 將三個下載下來的文件放在同一個目錄底下



![image1](images\image1.PNG)





### STEP 3: 在同一個目錄底下編寫HTML檔，並載入三個剛下載好的文件



+ 這邊要注意一下的是我跟大家下載下來的版本可能不同，所以要導入的文件名稱也會有所不同喔

```HTML
<!--
引用三份下載下來的文件，像是載入三個套件的感覺
-->

<script src = "jquery-3.5.1.min.js"></scrip>
<script src = "jquery.json2xml.js"></script>
<script src = "jquery.xml2json"></script>
```







### STEP 4: 開始撰寫JavaScript，來執行轉換 - XML 和 JSON 間互相轉換





#### XML 轉換 JSON步驟

+ $.xml2json: 將 XML 轉換成 JavaScript 對象
+ JSON.stringify: 將 JavaScript 轉換成JSON格式字符串



範例一: XML 轉換成 JSON

```HTML
<!--
引用三份下載下來的文件，像是載入三個套件的感覺
-->

<script src = "jquery-3.5.1.min.js"></scrip>
<script src = "jquery.json2xml.js"></script>
<script src = "jquery.xml2json.js"></script>


<script type = "text/javascript">

// XML格式的字符串
var xml_str = "<root>" +
                        "<name>Jack</name>" +
                        "<score>99</score>" +
                        "<friend>Jen</friend>" +
                        "<friend>Ken</friend>" +
                        "<friend>Cathy</friend>"+
                        "<friend>Cindy</friend>"+
                        "</root>";


console.log("XML Format: ", xml_str);

// XML 轉換成 JavaScript 對象
var javascript_obj = $.xml2json(xml_str);

console.log("JavaScript Object: ", javascript_obj);

// 將 JavaScript 對象轉換成 JSON 對象
var json_str = JSON.stringify(javascript_obj);

console.log("JSON Format: ", json_str);


</script>

```



![xml2json](images\xml2json.PNG)





#### JSON 轉換 XML 步驟

+ JSON.parse: 將 JSON 對象轉換成 JavaScript 對象 
+ $.json2xml: 將 JavaScript 對象轉換成 XML 格式的字符串



範例二:

```HTML
<!--
引用三份下載下來的文件，像是載入三個套件的感覺
-->

<script src = "jquery-3.5.1.min.js"></scrip>
<script src = "jquery.json2xml.js"></script>
<script src = "jquery.xml2json.js"></script>

<script type = "text/javascript">



// JavaScript對象
var Student = {
    name: "Jack",
    score: 99,
    Teacher: {
        name: "Jen",
        height: 178,
        weight: 70
    },
    run: function(){
        return 2
    },
    x: null,
    y: undefined


};

console.log("JavaScript Objec: ", Student);

// 將JavaScript對象轉換成XML
var xml_str = $.json2xml(Student);

console.log("XML Format: ", xml_str);


</script>
```





## 2. GeoJSON & TopoJSON 地理資訊


### GeoJSON

+ 說明: 基於JSON格式，用來描述地理空間資訊的數據交換格式，它定義了幾種類型的JSON對象(Object)，和它們組合於一起的方法，用來表示地理相關要素、屬性和空間範圍資料的資訊


+ 格式: 需符合JSON格式，但名稱上給了一些固定選擇和規則


+ 定義 GeoJSON 方法
    + GeoJSON 最外層是一個單獨的對象(Object)，而這個對象用來表示:
        + 幾何體 Geometry
        + 特徵 Feature
        + 特徵集合 FeatureCollection
    + 最外層的 GeoJSON 裡面包含了很多的子對象，而且每個子對象都具有一個 type 屬性，用來表示對象的類型，但 type 一定要是下面其中之一:
        + Point 點
        + MultiPoint 多點
        + LineString 線
        + MultiLineString 多線
        + Polygon 面
        + MultiPolygon 多面
        + GeometryCollection 幾何體集合
        + FeatureCollection 特徵集合
        + Feature 特徵



**重要規則**

如果 type 設定為

+ 第一種 - Point、MultiPoint、LineString、MultiLineString、Polygon、MultiPolygon : 必須有變量coordinates，也就是需要設定坐標
+ 第二種 - GeometryCollection(幾何體的集合): 必須有變量geometries，而它的值是一個數組(Array)，裡面的每一項都是一個 GeoJSON 幾何對象
+ 第三種 - Feature(特徵): 必須有變量 geometry 和 properties，geometry 的值必須是幾何體的對象，而 properties 表示特性，它的值可以是任何的 JSON 對象或是 null(空值)
+ 第四種 - FeatureCollection(特徵集合): 必須包含一個名稱為 features 的成員，而 features 的值是一個數組，而數組中的每一個元素為特徵對象



**實作**

+ 將撰寫好的 GeoJSON 複製到線上實現 GeoJSON工具(https://geojson.io/#map=2/20.0/0.0)，來查看結果






+ **第一種**

```JSON
1. 點對象
{
    "type": "Point",
    "coordinates": [-120, 66]
}

2. 線對象
{
    "type": "LineString",
    "coordinates": [[-120, 66], [-100, 28]]
}

3. 面對象
{
    "type": "Polygon",
    "coordinates": [ [ [28, 0], [36, 0], [36, 6], [28, 0] ] ]
}

```

分別執行結果

![geojson1](images\geojson1.PNG)

![geojson2](images\geojson2.PNG)

![geojson3](images\geojson3.PNG)





+ **第二種**






```JSON
{
    "type": "GeometryCollection",
    "geometries": [
        {
           "type": "Point",
           "coordinates": [120, 60]
        
        },
        {
            "type": "LineString",
            "coordinates": [ [100, 60], [100, 40] ]
         
        }
    ]
}
```
執行結果

![geojson4](images\geojson4.PNG)



+ 第三種

```JSON
{
    "type": "Feature",
    "properties": {
        "name": "HsinChu"
    },
    "geometry": {
        "type": "Point",
        "coordinates": [121, 24.82]
     
    }     
}
```

執行結果



![geojson5](images\geojson5.PNG)



### TopoJSON



+ 說明: 為 GeoJSON 依照拓樸學編碼後的擴展形式
+ 由鼎鼎大名的 D3.JS 視覺化套件作者 Mike Bostock 制定的
+ 和 GeoJSON 的區別: 相較於 GeoJSON 直接使用 Polygon、Point等的幾何體來代表圖形的方式，TopoJSON 則是透過共享體(arcs)整合而組合而成的幾何體圖形


+ 優勢: TopoJson 產出的文件更小，大概縮小了80%
+ 原因: 
    + 邊界線只會記錄一次 - 像是新竹和苗栗的邊界線只會記錄一次
    + 地理坐標是使用整數，而非浮點數





### 線上工具 - 實現 GeoJSON & TopoJSON



+ JSON 線上解析工具: http://json.cn/
+ 線上實現 GeoJSON 工具: https://geojson.io/#map=2/20.0/0.0
+ 轉換 GeoJSON 和 TopoJSON 工具: https://mapshare.qrg/
















