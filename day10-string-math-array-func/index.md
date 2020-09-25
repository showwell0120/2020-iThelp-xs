# [Day10] 內建函數 － 字串 / 數學 / 陣列

比較純資料處理的函數，像是字串處理、數學運算和陣列處理。這些函數的提供，可以幫助在程式上可以更專注在交易邏輯的實現上。

今天只會各舉 2、3 個函數來感受看看使用上的便利性。當之後開發腳本上覺得哪裡處理上比較麻煩的，就可以先去官方文件找找，看有沒有適合的內建函數可以用囉。

## 字串函數

### `Text(value1, value2, value3, ...)`

就像 Javascript 的`console.log`一樣，把各個變數組合成一個字串輸出。

```javascript
Variables: str("");
str = Text("Close=", close, " / ", "Close=", high, 111);
```

### `StrCompare(string1, string2, loose = true)`

比較兩個字串間是否相等。
第三個參數為選擇性參數，決定是否不區分大小寫。預設值為 `true`，表示大小寫不一定要相等。
另外回傳結果的代號為下

| 結果                 | 代碼  |
| -------------------- | ----- |
| string1 等於 string2 | **0** |
| string1 大於 string2 | **1** |
| string1 小於 string2 | **2** |

```javascript
// 主商品是台積電(2330.TW)
if StrCompare(symbol,"2330.tw",false) = 0
  then plot1(1)
else plot2(0);  // 這行會被執行到
```

## 數學函數

### `AvgList(value1, value2, value3, ...)`

取得傳入的數值群的平均值。

```javascript
// (開盤價 + 最高價 + 最低價) / 3
Value1 = AvgList(Open, High, Low);
```

要注意的是，如果要計算的是序列型資料的數值平均，則使用 `Average(序列, 期數)`。
序列型資料就是我們透過關鍵字。取得特定時間內的欄位資料，像是 close(收盤價)、high(最高價)等。

```javascript
//計算10期收盤價的移動平均
value1 = Average(Close, 10);
```

### `SumList(value1, value2, value3, ...)`

取得傳入的數值群的總值。

```javascript
// 計算平均價格
Value1 = SumList(Open, High, Low, Close) / 4;
```

要注意的是，如果要計算的是序列型資料的數值加總，則使用 `Summation(序列, 期數)`。

```javascript
//計算10期收盤價的總和
value1 = Summation(Close, 10);
```

### `Round(value, Decimalplaces)`

回傳四捨五入後的數值。並傳入小數位數決定留多少位。

```javascript
Value1 = Round(89.3453, 0); // Value1 = 89
Value2 = Round(89.783, 1); // Value1 = 89.8
Value3 = Round(89.1978, 2); // Value1 = 89.20
```

## 陣列函數

### `Array_Sum(array, startPosition, endPosition)`

取得陣列裡元素加總的數值。第一個位置的初始值為 `1`，以此類推。

```javascript
Array: arr[3](0); // 宣告arr是一個有3個元素的陣列，初始值都是0
arr[1] = 1;
arr[2] = 2;
arr[3] = 3;
Value1 = Array_Sum(arr, 1, 2); // Value1 = 3 (1 + 2)
Value2 = Array_Sum(arr, 1, 3); // Value2 = 6 (1 + 2 + 3)
```

### `Array_Sort(array, startPosition, endPosition, order:boolean)`

將陣列裡的元素進行大小排序。第一個位置的初始值為 `1`，以此類推。
除了要傳入資料陣列，還要設定排序的起始位置、結束位置跟排序機制。  
另外 `order` 的部分決定升冪或降冪。`true` 為升冪(小到大)；`false` 為降冪(大到小)。

```javascript
Array: arr[3](0); // 宣告arr是一個有3個元素的陣列，初始值都是0
arr[1] = 1;
arr[2] = 2;
arr[3] = 3;
Array_Sort(arr, 1, 5, true); // arr = [1, 2, 3]
Array_Sort(arr, 1, 5, false); // arr = [3, 2, 1]
```

## 小結

今天就到這邊  
Happy trading ! 明天見囉 !

## 參考資源

- [內建函數 - 字串函數](https://xshelp.xq.com.tw/XSHelp/lists?a=STRINGFUNC)
- [內建函數 - 數學函數](https://xshelp.xq.com.tw/XSHelp/lists?a=NUMBERFUNC)
- [內建函數 - 陣列函數](https://xshelp.xq.com.tw/XSHelp/lists?a=ARRAYFUNC)
