# [Day24] 實戰 - 看投信進出表時的技巧

## 影片在這裡

[![Yes](https://img.youtube.com/vi/7wMqzfyTdbE/0.jpg)](https://www.youtube.com/watch?v=7wMqzfyTdbE)

## 分類：`選股` `投信`

## 重點整理

- 找出投信買超的情況下，持續有所表現的股票
  1. 最近 5 天的成交量都超過 500 張
  2. 投信的買超增加，而且近 1 天佔超過 10％，前一天超過 5%
  3. 投信持股比例小於 1.5%
  4. 成交價與開盤價比超過 4%(當日收紅 K)

## 程式碼

```javascript
Input:SITCARatioThreshold(1.5);
Var:SITCA(0), SITCARatio(0), NetV(0), SVR(0);

SITCA = GetField("投信買賣超", "D");
SITCARatio = GetField("投信持股比例", "D");

NetV = V - GetField("當日沖銷張數", "D");

SVR = SITCA / NetV;

Condition1 = trueall(V > 500, 5);  // 最近 5 天的成交量都超過 500 張

Condition2 = SVR > SVR[1] and SVR >= 0.10 and SVR[1] > 0.05;  // 投信的買超增加，而且近 1 天佔超過 10％，前一天超過 5%

Condition3 = SITCARatio < SITCARatioThreshold;  // 投信持股比例小於 1.5%

Condition4 = (C-O) / O >= 0.04; // 成交價與開盤價比超過 4%(當日收紅 K)

Condition100=Condition1 and Condition2 and Condition3 and Condition4;
If Condition100 Then Ret=1;
```

## 參考資源

- [傳授看投信進出表時的技巧](http://www.xq.com.tw/videoteach//videoteach/%e5%82%b3%e6%8e%88%e7%9c%8b%e6%8a%95%e4%bf%a1%e9%80%b2%e5%87%ba%e8%a1%a8%e6%99%82%e7%9a%84%e6%8a%80%e5%b7%a7/)
