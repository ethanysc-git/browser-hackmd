瀏覽器: 多程序瀏覽器長什麼樣子
===

### 首先我們先來看看單程序的瀏覽器會長什麼樣子：   


![](https://hackmd.io/_uploads/B1Jz1ku15.png)
==非常早期的瀏覽器是單程序瀏覽器(Single Process)==

**你可以發現: 一個程序下運行多個不同功能的執行緒，而且他們彼此會互相影響，一個功能延遲就會拖累其他功能的運行，更別提當中發生崩壞時。**

******

### 多程序瀏覽器(Multi Processes)：   

![](https://hackmd.io/_uploads/BJolGk_J9.png)

==多程序瀏覽器主要解決了3個問題==

**1.  穩定性:
由於程序之間彼此是隔離的，所以當頁面中的某個功能或插件崩壞時，僅僅會影響到該部分，而不會造成整個頁面的癱瘓**

**2. 流暢度: 
因為JavaScript也運行在瀏覽器的渲染流程中，若是多程序的瀏覽器，當某個JavaScript渲染流程發生延遲或是阻塞時，網頁的其他部分或是其他頁面便不致於發生問題**

**3. 安全性: 
由於程序與程序之間有所隔離，某程序的敏感資料並不能被其他程序直接取用，若發生惡意程序的攻擊事件(如: 惡意的插件)，使用者便能得到多一分保障。**

:::info
**各瀏覽器程序簡介:**

**瀏覽器程序:**
主要負責介面顯示，用戶交互，子程序管理以及資料儲存等功能。

**渲染程序:**
核心任務是將HTML、CSS 和 JavaScript轉換成用戶可以交互之網頁
排版引擎Blink和JavaScript引擎V8都是運行在此
默認情況下，Chrome會為每一個分業創造一個渲染程序。
出於安全考量，渲染程序都是在沙盒環境下執行。

**GPU程序:**
UI介面的繪製(依照渲染程序的結果來執行)。

**網路程序:**
主要負責頁面網路資源的加載。

**插件程序:**
主要負責插件的運行，因為插件容易崩壞，所以主要透過插件程序來隔離。


:::


:::danger
**多程序瀏覽器的缺點:**
更高的記憶體佔用，更加複雜的系統結構（需要更多不同的程序之間的溝通）
:::



  
### 目前最多使用者的瀏覽器Chrome：   

==讓我們再回到一開始介紹的工作管理員畫面==

![](https://hackmd.io/_uploads/r1UBs1d15.png)

這次有所不同的是，我多開啟了一個分頁

==這便是上面所提及到的: 默認情況下，Chrome會為每一個分業創造一個渲染程序。==

在Google所公布的文檔中有提到，chrome總共有四種瀏覽器模式
分別是:

**- [Process-per-site-instance](https://www.chromium.org/developers/design-documents/process-models/#process-per-site-instance)**

**- [Process-per-site](https://www.chromium.org/developers/design-documents/process-models/#process-per-site)**

**- [Process-per-tab](https://www.chromium.org/developers/design-documents/process-models/#process-per-tab)**

**- [Single process](https://www.chromium.org/developers/design-documents/process-models/#single-process)**

**其中Process-per-site-instance為其預設之模式，優缺點如上述所提及的一樣**

**而Single process則是僅供測試及開發瀏覽器時所使用**

  
  
[參考資料: Inside look at modern web browser browsers](https://developers.google.com/web/updates/2018/09/inside-browser-part1)
[參考資料: The Chromium Projects](https://www.chromium.org/chromium-projects/)


###### tags: `書本模式`