# [Day14] 系統函數 - 邏輯判斷與技術指標

## 邏輯判斷

### `CrossOver` & `CrossUnder`

大家都聽過黃金交叉與死亡交叉。在認識他們之前，先了解一下什麼是 MACD 指標。

> MACD 稱為 **指數平滑異同移動平均線** ，是利用 **收盤價** 的 **短期與長期** 指數移動平均線之間的聚合與分離程度。是進出場作出研判的技術指標。

在短期與長期均線的分佈中  
如果短期均線向上，並與長期均線交叉，稱為 **黃金交叉**  
相反地，如果短期均線向下，並與長期均線交叉，則稱為 **死亡交叉**。

在 XS 中，我們可以透過 `CrossOver` 或 `CrossUnder` ，傳入兩個序列，來觀察兩個均線序列是否有達到黃金交叉或死亡交叉的情況。

```javascript
condition1 = CrossOver(Average(close, 5), Average(close, 10)); //判斷5期均線和10期均線是否黃金交叉
condition2 = CrossUnder(Average(close, 5), Average(close, 10)); //判斷5期均線和10期均線是否死亡交叉
```

### `TrueAll` & `TrueAny` & `TrueCount`

這三個函數都是拿來判斷條件式的符合狀況。第一個參數傳條件式，第二個則傳計算的期數。

- `TrueAll`：所有期數都符合條件，回傳布林值
- `TrueAny`：期數內只要有一筆符合即回傳 `true`，否則回傳 `false`
- `TrueCount`：回傳期數內符合條件式的次數

```javascript
condition1 = TrueAll(Close > Close[1], 3); //判斷K棒是否連續三期上漲
condition2 = TrueAny(Close > Close[1], 3); //判斷最近三期是否有任一期K棒上漲
value1 = TrueCount(close > close[1], 5); //計算過去5天連續收紅的次數
```

## 技術指標

在技術指標中，XS 有為許多技術分析的常用或重要的指標撰寫腳本，並成為系統函數之一。所以如果想從技術分析開始著手的也可以從這部分開始學習指標函數的應用。

### `MTM(期數)`

以當期收盤價減去前 N 期的收盤價，得出差距。也被稱為運動量指標。

```javascript
value1 = MTM(10); //計算收盤價10期的運動量指標
plot1(value1, "MTM");
```

### `AR(期數)`

計算買賣氣勢強度的測試指標，觀察開盤後股價的真實反應。

如果值在 **0.25~1.85** 之間，表示行情盤整中  
在 0.25 以下的話，表示行情低迷  
在 1.85 以上的話，表示行情很熱絡

```javascript
value1 = AR(26); //計算26期的AR指標
```

### `TechScore`

`TechScore` 是 XS 中使用多種指標計算出來的綜合分數。作為多空判斷。

分數會介於 **\*0~14** 之間
**12** 以上表示超買
**3** 以下表示超賣

使用的指標共有 14 種：

1. Arron 指標
2. 隨機漫步指標
3. 順勢指標
4. CMO 錢德動量擺動指標
5. RSI
6. MACD
7. MTM
8. KD
9. DMI
10. AR
11. ACC
12. TRIX
13. SAR
14. 均線

```javascript
value1 = TechScore; //計算多空判斷分數
plot1(value1, "多空指標");
```

## 參考資源

- [系統函數 - 邏輯判斷](https://xshelp.xq.com.tw/XSHelp/lists?a=LOGICFUNC)
- [系統函數 - 技術指標](https://xshelp.xq.com.tw/XSHelp/lists?a=TECHINDEXFUNC)
