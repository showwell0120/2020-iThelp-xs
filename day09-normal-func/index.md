# [Day09] 內建函數 － 一般函數

如果有看過前面的文章的話，其實已經對一般函數有基本認識囉!      
在[第6天](https://ithelp.ithome.com.tw/articles/10241426)介紹的輸出函數(`Print` / `Plot` / `RaiseRunTimeError`)，就是屬於一般函數。    

一般函數通常是用來設定執行環境，或指定系統產出想要的東西。    
今天我們就再來認識幾個一般函數看看吧！ 

## `BarFreq` & `BarInterval`

`BarFreq` 是取得目前腳本執行的頻率。回傳內容可參考[第8天](https://ithelp.ithome.com.tw/articles/10242830)的頻率說明表格。

`BarInterval`則是取得回傳目前腳本執行的**分鐘頻率間隔**。如果目前執行頻率不是分鐘的話，則一律回傳 **1**。

通常這兩個會組合在一起來加強判斷頻率。

```javascript
// 判斷是30分鐘線
If BarFreq = "Min" and BarInterval = 30 Then
  Begin
    //...
  End;
```

```javascript
//資料是日線才往下執行
if BarFreq <> "D" then return;
```

## `SymbolType`

回傳目前執行腳本的商品類型代碼。

| 商品類型      | 代碼   |
| --------- | ------ |
|指數|**1**|
|股票|**2**|
|期貨|**3**|
|權證|**4**|
|選擇權|**5**|
|轉債|**6**|

```javascript
switch(SymbolType)
  begin
    case 1: //...
    case 2: //...
    case 3: //...
    case 4: //...
    case 5: //...
    case 6: //...
  end;
```

## 小結

今天大致先介紹基本的函數使用，其實裡面還有蠻多函數是在做資料讀取的控制。這部分有興趣的話可以先看[這篇](http://www.xq.com.tw/lesson/xspractice/%E8%B3%87%E6%96%99%E8%AE%80%E5%8F%96%E7%AF%84%E5%9C%8D%E8%88%87%E8%85%B3%E6%9C%AC%E5%9F%B7%E8%A1%8C%E7%9A%84%E9%97%9C%E4%BF%82/)，有機會的話之後會再提到喔。

今天就到這邊    
Happy trading ! 明天見囉 !

## 參考資源

- [內建函數 - 一般函數](https://xshelp.xq.com.tw/XSHelp/lists?a=GENERALFUNC)
