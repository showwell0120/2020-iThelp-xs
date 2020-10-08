# [Day23] 實戰 - 掌握代操資金看上的股票

## 影片在這裡

[![Yes](https://img.youtube.com/vi/SJwWoCZMlb8/0.jpg)](https://www.youtube.com/watch?v=SJwWoCZMlb8)

## 分類：`選股` `投信` `籌碼`

## 重點整理

- XQ 裡有個獨特的資料欄位 - **綜合前十大券商買賣超張數**，每天系統會把十大券商總公司的買賣超張數加總起來
- 近年來勞退基金給投信代操的資金有增加趨勢
- 代操並不會歸類在投信買賣超，但通常投信的單子下在常往來券商，券商再下給法人部門，而法人部通常是在總公司。所以這個欄位可以當作代操基金的量
- 找出衡量的標準：
  1. 最近大盤表現不好
  2. 綜合前十大券商買賣超張數在過去三天的金額都超過 2000 萬
  3. 綜合前十大券商買賣超張數在最近一天的金額超過 2.5 億
  4. 是股本小的公司
  5. 股價斜率近期是攀升

## 程式碼

`linearregslope(序列,期數)`: 以序列的特定期數資料分佈，算出線性迴歸的斜率。

```javascript
Input:TSELen(15);
Input:PeriodYear(3);
Var:DAO(0), TSEBias(0), StockBias(0);

// 投信代操買賣超金額
DAO = GetField("綜合前十大券商買賣超張數", "D") * 0.1 * (O * 2 + H + L + C * 2) / 6;

Condition1 = GetSymbolField("TSE.TW", "收盤價") < average(GetSymbolField("TSE.TW", "收盤價"), TSELen) ;  // 加權指數於15日均線下方

Condition2 = trueall(DAO > 2000, 3);  // 連續三日綜合前十大券商買賣超金額>2000萬

Condition3 = DAO > 25000;  // 今日綜合前十大券商買賣超金額>2.5億

Condition4 = GetField("股本(億)", "D") < 100;  // 股本<100億

Condition5 = linearregslope(C, 8) > 0; // 8日收盤斜率>0

Condition100 = Condition1 and Condition2 and Condition3 and Condition4 and Condition5;
If Condition100 Then Ret=1;
```

## 參考資源

- [如何掌握代操資金看上的股票](http://www.xq.com.tw/videoteach//videoteach/%e5%a6%82%e4%bd%95%e6%8e%8c%e6%8f%a1%e4%bb%a3%e6%93%8d%e8%b3%87%e9%87%91%e7%9c%8b%e4%b8%8a%e7%9a%84%e8%82%a1%e7%a5%a8/)
- [LinearRegSlope - (系統函數) 趨勢分析](https://xshelp.xq.com.tw/XSHelp/?HelpName=LinearRegSlope&group=TRENDFUNC)
