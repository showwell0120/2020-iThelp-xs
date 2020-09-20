經過昨天的介紹後，知道 XS 的重點其實就是建立在時間序列上進行邏輯運算。   
接下來再來整理語法上基本的組成跟結構。

## 運算子

這部分對學過程式的應該很快就上手！所以就條列式說明   
- 數學運算子： `+` 、 `-` 、 `*`、 `/` 、 `=` 
- 關係運算子：`>` 、 `<` 、 `<=` 、 `>=` 、 `<>`(不等於)
- 邏輯運算子： `and` 、 `or` 、 `not`

來練習看看吧！

```javascript
// 近一日漲幅超過5% 且超過前一日成交量
volume>volume[1] and
close/close[1]>1.05
```

## 標點符號

這邊我偷懶一下，，因為我家大大整理得很完整，所以直接拿來給大家看看
![img](http://cdn.xstrader.net/wp-content/uploads/2015/05/%E6%A8%99%E9%BB%9E%E7%AC%A6%E8%99%9F.jpg)

其中比較需要注意的地方是，`//` 跟 `{}` 的差別。   
就跟一般程式語言一樣，可以允許有單行註釋跟多行註釋，所以 `//` 主要用於單行 ; 而 `{}` 在其他語言中常是用來包覆一個程式區塊，在這裡則是註釋的用途。

我們拿範例來練習一下

```javascript
{
    這裡是註釋，不會被執行到
    收盤價
    等於開盤價且
    等於最高價且
    最高價減最低價大於前一天的最高價減最低價後2倍
}
Close=open and close=high
And (high-low)>(high[1]-low[1]）*2
```

## 忽略字

XS 跟隨元老級的交易平台 Tradestation 的精神，希望能夠讓沒有程式背景的投資人可以像寫文章般輕鬆上手。所以 XS 建立了一些忽略字，大多都是英文中的量詞、連接詞、介系詞，讓系統遇到這些字時可以不執行，幫助投資人在寫腳本時可以更直覺。

以下也是大大整理好的相關表格，可以請大家看看

![img](http://cdn.xstrader.net/wp-content/uploads/2015/10/102203.png)

一樣拿範例程式比較看看

```javascript
// 收盤價突破二十日移動平均時

// 有忽略字 - was, over
if close was cross over the average(close,20)
then ret=1;

// 無忽略字
if close cross over average(close,20)
then ret=1;
```

## 小結

認識完今天的介紹後，我們大約就可以看懂一半以上的語法了！   
明天繼續來認識新語法～

今天就到這邊
Happy trading ! 明天見囉 !

## 參考資源

- [XS 學習地圖](https://xstrader.net/xslearnmap/)
- [for 程式交易初學者的七堂課](https://xstrader.net/for%e7%a8%8b%e5%bc%8f%e4%ba%a4%e6%98%93%e5%88%9d%e5%ad%b8%e8%80%85%e7%9a%84%e5%85%ab%e5%a0%82%e8%aa%b2/)
