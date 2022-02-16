渲染流程:分層
===

### 渲染流程:分層   

![](https://hackmd.io/_uploads/BJqZhAFJ9.png)


:::info
讓我們快速回顧一下瀏覽器執行的所有步驟:

1. 處理HTML，產生DOM結構
2. 處理CSS，產生CSSOM結構
3. 將DOM和CSSOM合併為Render tree
4. 對Render tree進行版面配置(生成Layout Tree)
5. 將結果繪製在螢幕上
:::

![](https://hackmd.io/_uploads/BJrc30Y19.png)


在流程4和流程5之間，其時還存在一個分層的動作
在網頁畫面中，常常存在很多複雜的效果: 3D動畫、使用者滾動頁面、圖片的顯示順序等等，為了更方便地實現這些效果，渲染引擎還需要用Layout Tree來生成對應的Layer Tree

![](https://hackmd.io/_uploads/ByIsq0Kkq.png)

在Paint Records完成之後，Renderer Process會將接下來的工作交給Compositor Thread

### Compositor Thread:   
Compositor Thread會將上述需要繪製的圖層切割成更小的圖塊(tiles)，而這些更小的圖塊會再交給更下一層的**raster threads**來處理
**raster threads** 會將這些圖塊存放到瀏覽器的GPU儲存空間裡，
Compositor Thread會匯整這些處理資訊(draw quads)，透過IPC來送給 Browser Process，最後送到GPU去顯示到畫面上(前者為繪圖資料，後者為繪圖指令)。


![](https://hackmd.io/_uploads/H1u7MJ515.png)

![](https://hackmd.io/_uploads/Bk9LMJ51c.png)

### 渲染流程圖   

**整個渲染流程可以用下面這張圖來表示**


![](https://hackmd.io/_uploads/H1kna1ck9.png)



    
[參考資料: How Browsers Work: Behind the scenes of modern web browsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)

[參考資料: Constructing the Object Model ](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/constructing-the-object-model)
###### tags: `書本模式`