# [Day13] 系統函數 - 分析

## 統計分析

### `StandardDev(序列,期數,類型)`

以最新的資料數值為基準，計算在序列中，過去期數的標準差。用來表示此期數範圍的分散程度。

在類型的參數中，傳入標準差類型的代號

| 標準差類型 | 代碼  |
| ---------- | ----- |
| 母體標準差 | **1** |
| 樣本標準差 | **2** |

關於母體跟樣本的差別可以參考[這篇](https://www.researchmfg.com/2016/07/sigma-n-1/)。

```javascript
value1 = StandardDev(close, 20, 2); //計算過去20期收盤價的標準差
```

### `Correlation(序列1,序列2,期數)`

以最新的資料數值為基準，計算兩個序列在過去期數的相關係數，用來表示這兩個序列的線性相關程度。

回傳值介於 **1~-1** 之間。

```javascript
value1 = GetField("外資買賣超金額");
value2 = rateofchange(close, 1); //計算當日漲跌幅
value3 = Correlation(value1, value2, 20); //計算過去20期外資買賣超金額與大盤漲跌幅的相關係數
plot1(value3);
```

## 趨勢分析

### `TSELSindex(期數,標準)`

利用 **外資買賣超金額**，計算大盤的多空狀態。這個系統函數是由公司大大寫的，詳細的判斷邏輯可以參考[這篇](https://xstrader.net/%E6%89%93%E9%80%A0%E8%87%AA%E5%B7%B1%E7%9A%84%E5%A4%A7%E7%9B%A4%E5%A4%9A%E7%A9%BA%E5%87%BD%E6%95%B8/)。

函數的概念上是，只要外資有連續買超，則大盤多頭的機率會比較高。

如果在某個期數範圍內，外資買超的的期數超過標準，則回傳**1**，否則回傳**0**。

```javascript
tselsindex(10, 7); // 過去10期中至少有7期外資的買超
```

### `SwingHigh` & `SwingHighBar`

這組函數還有對應的 `SwingHigh` 跟 `SwingLowBar`。主要是取得目標範圍內的轉折高/底點的價格或 K 棒。

以 `SwingHigh`為例，依序要傳入五個參數 -

- 序列：通常是開高低收的價格序列
- 期數：尋找轉折點的樣本期數
- 左肩期數：高點左側要有幾筆較低的數值
- 右肩期數：高點右側要有幾筆較低的數值
- 第幾個高點：1 為最近一次的高點、2 為第二近的高點

如果無法找到目標，回傳值為 **-1**。

```javascript
value1 = SwingHigh(High, 20, 3, 3, 2); //找出過去20期內，第2個轉折高點
```

## 小結

今天就到這邊  
Happy trading ! 明天見囉 !

## 參考資源

- [系統函數 - 統計分析](https://xshelp.xq.com.tw/XSHelp/lists?a=STATSFUNC)
- [系統函數 - 趨勢分析](https://xshelp.xq.com.tw/XSHelp/lists?a=TRENDFUNC)
