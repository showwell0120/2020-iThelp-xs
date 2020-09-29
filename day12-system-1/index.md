# [Day12] 系統函數 - 價格

在系統函數中，XS 有針對資料數值定義關鍵字，並且對常見或比較複雜的運算建立函數。跟內建函數的用意一樣，都是幫助使用者以輕鬆的方式寫出變化更多的策略。

今天來看的是跟價格有關的系統函數。

## 價格取得

### `AvgPrice`

取得以某根 K 棒的開高低收，四個數字計算出來的平均價格。如果要取前 N 期的數值，則以中括號 `[N]` 加在後面即可。

```javascript
plot1(avgprice); //繪製當天平均價格的連線
plot2(avgprice[1]); //繪製前一天平均價格的連線
```

### `CloseD` / `CloseW` / `CloseM` / `CloseQ`/ `CloseH` / `CloseY`

在開盤價(Open)、最高價(High)、最低價(Low)跟收盤價(Close)，最常聽到的是以交易日為單位的數值。不過在透過時間長度的控制，我們也可以取得範圍內有關某種價格的平均價。

其中，時間長度可為週 / 月 / 季 / 半年 / 年。由這些時間長度組合開高低收，就組合出像 `CloseD` / `CloseW` / `CloseM` 等等函數直接可以使用，而不用自己還需計算日期跟加總平均。

在參數中，繪製當期的話則傳 `0`；繪製前 N 期的話則傳 `N`。

```javascript
plot1(CloseD(0)); //繪製當日收盤價的連線
plot2(CloseD(1)); //繪製前一日收盤價的連線
```

### `Highest` / `Lowest`

回傳序列資料中的極值。

在第一個參數傳入序列（例如：high, close, ...）；第二個參數則傳要計算的期數。

```javascript
plot1(Highest(high, 5)); //繪製5期最高價的最大值的連線
```

### `TrueHigh` / `TrueLow`

在認識真實高點、真實低點前，可以先往下到 **TrueRange**了解什麼是**真實區間**喔。

取得價格真實區間(TrueRange)的高點或低點。如果要取前 N 期的數值，則以中括號 `[N]` 加在後面即可。

```javascript
plot1(TrueHigh); //繪製當期真實區間高點的連線
plot2(TrueLow[1]); //繪製前一期真實區間低點的連線
```

## `WeightedClose`

計算公式為：(最高價 + 最低價 + 2\*當期收盤價)/4

取得加權平均收盤價(收盤價有較大的權重)。著名的 **MACD 指標** 即是利用這個數值做計算。如果要取前 N 期的數值，則以中括號 `[N]` 加在後面即可。

```javascript
plot1(WeightedClose); //繪製當期加權平均收盤價的連線
plot2(WeightedClose[1]); //繪製前一期加權平均收盤價的連線
```

## 價格計算

### `Average(序列, 期數:number)`

計算序列資料的**移動平均(MA)**。通常序列會是開高低收等價格序列。

```javascript
value1 = Average(Close, 5); //計算5期收盤價的移動平均
```

### `TrueRange`

Average True Range(ATR)是韋爾達先生提出觀測量價格波動性的方法。根據他的定義，先取得三種當期的特定兩個價格之間的幅度 -

- **最高價**與**最低價**的幅度
- **最低價**與**昨日收盤價**的幅度
- **最高價**與**昨日收盤價**的幅度

接著再取這三個數值中的最大值，作為 True Range(真實區間)。通常在程式交易中，會拿來做停損停利的依據。

在 XS 中，直接以 `TrueRange` 即可取得當期 K 棒的真實區間。如果要取前 N 期的數值，則以中括號 `[N]` 加在後面即可。

```javascript
plot1(TrueRange); //繪製當期K棒真實區間的連線
plot2(TrueRange[1]); //繪製前一期K棒真實區間的連線
```

## 小結

藉由這些系統函數的認識，其實也可以同時了解技術分析上的領域知識喔！所以大家也可以直接到官方文件上看看喔。

今天就到這邊
Happy trading ! 明天見囉 !

## 參考資源

- [系統函數 - 價格取得](https://xshelp.xq.com.tw/XSHelp/lists?a=PRICEGETFUNC)
- [系統函數 - 價格計算](https://xshelp.xq.com.tw/XSHelp/lists?a=PRICECULFUNC)
- [Average True Range(ATR)](https://eggeggfifa.pixnet.net/blog/post/87889095-atr-average-true-range-%E7%9C%9F%E5%AF%A6%E6%B3%A2%E5%8B%95%E5%8D%80%E9%96%93)
