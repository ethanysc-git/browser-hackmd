瀏覽器的主角:渲染引擎
===

### 渲染引擎的工作流程：   


![](https://hackmd.io/_uploads/HyiP9kGk5.png)

**下圖以WebKit為例:**

![](https://hackmd.io/_uploads/ryI6q1fyc.png)

- 渲染引擎讀取HTML後生成DOM Tree
- 讀取HTML中的CSS Link Tag來產生CSSOM Tree
- 用DOM Tree與CSSOM Tree合成Render Tree
- 基於Render Tree產成Layout Tree，負責各元素大小與位置的計算
- 最後由GPU劃出畫面


******
```
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <link href="style.css" rel="stylesheet">
    <title>Critical Path</title>
  </head>
  <body>
    <p>Hello <span>web performance</span> students!</p>
    <div><img src="awesome-photo.jpg"></div>
    <script src="app.js"></script>
  </body>
</html>
```
***以上為一段簡單的HTML程式碼，用作下方渲染引擎工作流程演示之依據***  
### 渲染引擎的工作流程演示：   

![](https://hackmd.io/_uploads/H1oZGgfyc.png)

**1. 轉換: 
    瀏覽器讀取HTML，然後根據指定的檔案編碼格式 (例如 UTF-8)，將其轉換為相應字元。**
**2.  詞法分析: 
根據W3C HTML5標準將之轉換為相對的「物件」。**
**3. DOM 建構: 
將建立的物件依照層級在樹狀資料結構中連結起來。**

==瀏覽器在建構這個簡單網頁的DOM時，在文件的head區段會遇到一個link標記==

**這是一個參照外部資源的CSS樣式表 
style.css:**
```
body { font-size: 16px }
p { font-weight: bold }
span { color: red }
p span { display: none }
img { float: right }
```
**與處理 HTML時非常類似的過程:**
最後會形成 :arrow_forward: 

![](https://hackmd.io/_uploads/ryZxLgMy9.png)

==瀏覽器會將這兩個結構合併==

![](https://hackmd.io/_uploads/r1jtLgfJq.png)



- 需要特別注意的事:
1. 某些節點可以透過CSS設定特別屬性(如: display:none)，從而在該轉譯的過程中被省略(不會出現在Render Tree中)。
2. 由於JavaScript可以為 DOM 新建元素、設計新元素樣式，以及附加或移除新元素，所以當瀏覽器讀到JavaScript(如: 本例中的app.js)，他會先暫停原本DOM的建構，轉而先執行JS的相關動作，避免白做工。

==進行到此時==

瀏覽器為了計算出每個物件的準確大小和位置，會開始從轉譯樹狀結構的根節點開始瀏覽，以計算網頁上每個物件的幾何形狀。

![](https://hackmd.io/_uploads/SySsoxGy9.png)

==即是上方圖式中的: Layout==

我們以下方的程式碼來做個簡單的理解:
```
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Critial Path: Hello world!</title>
  </head>
  <body>
    <div style="width: 50%">
      <div style="width: 50%">Hello world!</div>
    </div>
  </body>
</html>
```
![](https://hackmd.io/_uploads/r1eL3ef15.png)

**在知道哪些節點可見、計算的樣式和幾何形狀之後，我們便可以將這些資訊轉換為螢幕上的實際像素。這個步驟通常稱為「繪製」。**





:::info
讓我們快速回顧一下瀏覽器執行的所有步驟:

1. 處理HTML，產生DOM結構
2. 處理CSS，產生CSSOM結構
3. 將DOM和CSSOM合併為Render tree
4. 對Render tree進行版面配置(生成Layout Tree)
5. 將結果繪製在螢幕上
:::
    
[參考資料: How Browsers Work: Behind the scenes of modern web browsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)

[參考資料: Constructing the Object Model ](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/constructing-the-object-model)
###### tags: `書本模式`