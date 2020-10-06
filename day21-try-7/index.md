# [Day21] 實戰 - 超前佈署的法說會行情交易策略

## 影片在這裡

[![Yes](https://img.youtube.com/vi/rYE-uvSLAz4/0.jpg)](https://www.youtube.com/watch?v=rYE-uvSLAz4)

## 分類：`選股` `法說會`

## 重點整理

- 公司公布半年財報同時，通常會伴隨著法說會進行
- 針對即將法說會的選股策略，主要有以下的條件
  1. 過去 5 天內，成交量都大於 500 張
  2. 在 14 天內會舉行法說會
  3. 3 天內主力買超的總量，與成交量相比要超過 2%，且今天的主力買超是 3 天內最大的 -> 主力愈買愈多
  4. 關鍵券商買超 -> 大股東偏多
  5. 近一週與前一週比，千張大戶的的持股比例增加 ->大戶買進
  6. 今天的最高價創 8 天內的新高
- 如果符合標的偏少，可以盤中大戶買賣超取代關鍵券商和大戶持股等條件，以盤中的價量即時判斷

## 程式碼

```javascript
Condition1 = trueall(V > 500, 5);  // 過去 5 天內，成交量都大於 500 張

Condition2 = DateDiff(GetField("法說會日期"), Date) < 14
         and DateDiff(GetField("法說會日期"), Date)>0;  // 在 14 天內會舉行法說會

Condition3 = summation(GetField("主力買賣超張數","D"),3) > 0.02 * summation(V,3)
         and GetField("主力買賣超張數","D") = Highest(GetField("主力買賣超張數","D"),3);
         // 3 天內主力買超的總量，與成交量相比要超過 2%，且今天的主力買超是 3 天內最大的


Condition4 = GetField("關鍵券商買賣超張數","D") > 0;  // 關鍵券商買超

Condition5 = GetField("大戶持股比例","W",param := 1000) > GetField("大戶持股比例","W",param := 1000)[1];  // 近一週與前一週比，千張大戶的的持股比例增加

Condition6 = H > Highest(H[1],8);  // 今高創8日新高

Condition100 = Condition1 and Condition2 and Condition3 and Condition4 and Condition5 and Condition6;

// 篩選
If Condition100 Then Ret=1;  // 所有條件都符合，觸發警示通知
```

## 參考資源

- [超前佈署的法說會行情交易策略](http://www.xq.com.tw/videoteach//videoteach/%e8%b6%85%e5%89%8d%e4%bd%88%e7%bd%b2%e7%9a%84%e6%b3%95%e8%aa%aa%e6%9c%83%e8%a1%8c%e6%83%85%e4%ba%a4%e6%98%93%e7%ad%96%e7%95%a5/)
