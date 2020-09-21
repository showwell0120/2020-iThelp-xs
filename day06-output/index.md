# [Day06] 輸出

從第三天到昨天，我們都在學語法的組成結構、基本的運算指令，與組織流程。但是寫 XS 最主要的目的，就是要取得運算的結果，並且根據我們的目的，提供適當的功能，像是觸發通知、資料呈現等等。

因此，在 XS 中有提供四大主要的輸出函數，在程式運行結束時，可以輸出內容。

![png](http://cdn.xstrader.net/wp-content/uploads/2015/05/07_%E8%BC%B8%E5%87%BA%E8%AA%9E%E6%B3%95_1.png)

## `RetVal`

當程式運算過後符合腳本的條件，最重要的就是即時地讓我們知道系統的執行結果。因此 **`RetVal`** 就是一個讓系統知道說要不要發出通知訊號的 flag 變數。

RetVal 是 Return Value 的縮寫。撰寫時也能寫成 `ret`。
`RetVal=1`，表示觸發警示通知；
`RetVal=0`，則表示不觸發。

看個例子吧。

```javascript
if close>150 then ret=1;  // 如果收盤價高於150則觸發警示通知
```

## `Plot<1,2, ...>(expression, name)`

在 XQ 的技術分析中，可以選擇自訂指標的方式，將自己撰寫的繪圖邏輯印在副圖上。而繪圖的實作也是靠 XS 語法來輸出。

使用 `Plot<1,2, ...>(expression, name)`，將陳述式跟指標名稱分別帶入。在一個腳本內可以執行多個繪圖函式。

舉個官網例子看看。

```javascript
plot1(high - low, "K棒總長度");
plot2(close - open, "K棒柱子長度");
```

![png](http://cdn.xstrader.net/wp-content/uploads/2015/05/OUTPUT3.png)

## `Print(value1, value2, value3, ...)`

當你想取得特定資料作為研究、改善腳本、訓練模型用時，可以使用 `Print`，把想要的欄位一一帶入，當執行到這行時，系統會在本機產生一份 csv 檔。

以官網例子來看使用情境吧！

```javascript
// 用RSI黃金交叉來作為買進訊號，觀察隔天上漲的機率高低
// RSI: 某段時間內平均漲幅與平均跌幅所算出的數值。是個可看出股票價格強弱勢的指標
value1=rsi(close,5);
value2=rsi(close,10);
if value1[1] crosses above value2[1]
then print("前一日rsi黃金交叉", date, close-close[1])
```

存在本機的檔案以 excel 打開，大概就像這樣

![png](http://cdn.xstrader.net/wp-content/uploads/2015/05/OUTPUT7.png)

## `RaiseRunTimeError(interruptMsg)`

如果有些腳本只適合以特定頻率執行，或是有機會出現運算上的失誤，例如除數有可能為 0 等情況。為了可以讓系統執行時不被意外狀況卡住，就能使用 `RaiseRunTimeError(interruptMsg)`，並傳入訊息字串告知使用者相關的問題描述。

例如，如果這個腳本只適合以 5 分以內的分鐘線以內的頻率執行，在程式第一行就可以這樣寫

```javascript
if barfreq <> "Min" or barinterval > 5 then RaiseRunTimeError("請設定頻率在5分以內")
```

輸出訊息的示意圖

![png](http://cdn.xstrader.net/wp-content/uploads/2015/05/OUTPUT9.png)

## 小結

今天了解到在程式的最後，我們如何根據需求，使用各種輸出的函數，希望對大家都有幫助。

今天就到這邊  
Happy trading ! 明天見囉 !

## 參考資源

- [輸出語法](http://xstrader.net/%E8%BC%B8%E5%87%BA%E8%AA%9E%E6%B3%95/)
- [技術分析 RSI](https://www.jihsun.com.tw/md/event/jsun_school/stock10.html)
