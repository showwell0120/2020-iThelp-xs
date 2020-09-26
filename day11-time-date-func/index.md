# [Day11] 內建函數 － 時間 / 日期

在 XS 的內建函數中，有關於時間處理的函數，分為兩大類

- 時間函數：一日以內的時間單位，包括秒、分鐘、小時的顯示、轉換與運算
- 日期函數：以日為最小單位的日期處理

接著就來認識這些函數吧！

## 時間函數

### 時間單位

在有些函數中，我們會需要帶入時間的單位去進行運算。以下是各時間長度上的代碼

| 時間長度 | 代碼  |
| -------- | ----- |
| 秒       | **S** |
| 分鐘     | **M** |
| 小時     | **H** |

另外，在時間的表達上，通常格式為 **HHMMSS** 的數字，其中

- HH: 範圍是 **0~23**(可個位數帶入)
- MM: 範圍是 **00~59**
- SS: 範圍是 **00~59**

### `TimeDiff(time1:number, time2:number, unit)`

計算兩個時間點 `time1` 跟 `time2`的差距，並以第三個傳入的參數為回傳的數值單位。

另外，如果 `time2` 的數值比較大，也就是比`time1`來得晚的話，回傳的數值就會是負數。

```javascript
// 13點30分0秒 減 12點30分0秒 等於 60（分鐘）
Value1 = TimeDiff(133000, 123000, "M");

// 12點30分0秒 減 13點30分0秒 等於 -0.5（小時）
Value2 = TimeDiff(123000, 130000, "H");
```

來看實際應用的例子

```javascript
// 計算大單成交的時間間隔

Var: vTime(0);
If Volume*Close > 10000000 then vTime =Time; // vTime為交易金額大於1000萬的K棒時間
If TimeDiff(vTime, vTime[1], "M") < 5 Then Ret=1;  // 發生的很密集(5分以內)的話則觸發警示
```

### `TimeAdd(time:number, unit, integer:number)`

以 `time` 的時間為基準，加上 `integer`的數值計算，取得更早以前或更晚以後的時間數值。

回傳的數值也會是以 **HHMMSS** 為格式的數字。

```javascript
// 12點 加 1小時 等於 13點(130000)
Value1 = TimeAdd(120000, "H", 1);

// 12點30分0秒 減 30分 等於 12點(120000)
Value2 = TimeAdd(123000, "M", -30);
```

套一下情境感受看看

```javascript

// 取得當日創新高的時間點
HighTime ＝ //...

// 如果時間在創新高後的1小時內
if HighTime > 0 And Time > HighTime And Time < TimeAdd(HighTime,"H",1) Then
Begin
   //...
End;
```

## 日期函數

### `CurrentDate`

取得當前時間，回傳 8 位數的日期數值。

```javascript
Print(CurrentDate); // 20200926
```

### `DateToString(date:number)`

將傳入的日期數值 `date`，轉成格式為 **YYYY/MM/DD** 的字串。

```javascript
Print(DateToString(CurrentDate)); // 2020/09/26
```

## 小結

今天就到這邊  
Happy trading ! 明天見囉 !

## 參考資源

- [內建函數 - 時間函數](https://xshelp.xq.com.tw/XSHelp/lists?a=TIMEFUNC)
- [內建函數 - 日期函數](https://xshelp.xq.com.tw/XSHelp/lists?a=DATEFUNC)
