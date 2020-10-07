# [Day22] 實戰 - 找出主力買超而融券增加的股票

## 影片在這裡

[![Yes](https://img.youtube.com/vi/DiVBgbBqnn8/0.jpg)](https://www.youtube.com/watch?v=DiVBgbBqnn8)

## 分類：`選股` `主力` `融券`

## 重點整理

- **融券賣出(放空股票)**：投資人預期某檔價格會下跌，但沒該持股時，向券商借股票來賣出。這時預期會賣在高點，並在未來股價下跌後以低價買進
- **融券回補**：買回股票還給券商，期限為半年
- **融券使用率**：融券餘額佔融券限額的比例
- 主力積極作多，可是市場呈現放空時，以作多方式進場
- 策略需同時滿足以下條件：
  1. 融券最後回補日介於 15 ～ 100 天
  2. 3 天來的主力買超超過成交量的 8 成
  3. 融券餘額張數創 5 日新高
  4. 融券使用率創 5 日新高
  5. 今日收盤價創 5 日來的新高，且漲幅超過 3%的紅 K，且上引線(最高價-收盤價)的差距不到 0.01
  6. 大盤漲過均線(8)

## 程式碼

```javascript
Condition1 = trueall(V>500, 5);

// 融券最後回補日介於 15 ～ 100 天
Condition2 = DateDiff(GetField("融券最後回補日"), Date) < 100
and DateDiff(GetField("融券最後回補日"), Date) > 15;

// 3 天來的主力買超超過成交量的 8 成
Condition3 = summation(GetField("主力買賣超張數", "D"), 3) > 0.08 * summation(V, 3);

// 融券餘額張數創 5 日新高
Condition4 = GetField("融券餘額張數", "D") = Highest(GetField("融券餘額張數", "D"), 5);

// 融券使用率創 5 日新高
Condition5 = GetField("融券使用率", "D") = Highest(GetField("融券使用率", "D"), 5);

// 今日收盤價創 5 日來的新高，且漲幅超過 3%的紅 K，且上引線(最高價-收盤價)的差距不到 0.01
Condition6 = C > Highest(H[1], 5) and (C - O) / O > 0.03 and ( H - C) / C < 0.01;

// 大盤漲過均線(8)
Condition7 = CCT_TSE_Trend(8) = 1;

Condition100 = Condition1 and Condition2 and Condition3 and Condition4 and Condition6 and Condition7;

// 篩選
If Condition100 Then Ret=1;
```

## 參考資源

- [找出主力買超而融券增加的股票](http://www.xq.com.tw/videoteach//videoteach/%e6%89%be%e5%87%ba%e4%b8%bb%e5%8a%9b%e8%b2%b7%e8%b6%85%e8%80%8c%e8%9e%8d%e5%88%b8%e5%a2%9e%e5%8a%a0%e7%9a%84%e8%82%a1%e7%a5%a8/)
- [什麼是融券交易？融券利息、維持率、回補怎麼計算？](https://rich01.com/how-margin-short-stock/)
