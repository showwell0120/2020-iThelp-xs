# [Day26] 實戰 - 下降旗形且法人買超選股法

## 影片在這裡

[![Yes](https://img.youtube.com/vi/M01h2X1Lm4A/0.jpg)](https://www.youtube.com/watch?v=M01h2X1Lm4A)

## 分類：`選股` `型態`

## 重點整理

- 強勢股：之前呈上漲，但是因為獲利回吐的賣壓或消息面的改變，回檔整理後，又因主要利多的原因開始上漲
- 下降旗形：
  1. 多發生在空頭走勢中的整理階段
  2. 整理期間的高低點不斷上升，但成交量卻無法隨之增加時，而形成量價背離時，易形成下降旗形
     ![img](https://i1.kknews.cc/SIG=ilk10u/7qn0008570o063r6678.jpg)

## 程式碼

- `highestbar(序列, 期數)`: 在過去特定期數的範圍內，計算序列資料的最大值的所在 K 棒。
- `lowestbar(序列, 期數)`: 在以過去特定期數的範圍內，計算序列資料的最小值的所在 K 棒。
- `highest(序列, 期數)`: 在過去特定期數的範圍內，計算序列資料的最大值
- `lowest(序列, 期數)`: 在以過去特定期數的範圍內，計算序列資料的最小值

```javascript
input:period(30);  // 計算期間

value1 = highestbar(high, period);  // 找出這期間最高點在第幾根BAR

value2 = lowestbar(low, period);  // 找出這期間最低點在第幾根BAR

value3 = highest(high, period);  // 找出期間最高點

value4 = lowest(low, period);  // 找出期間最低點

if value2 > value1 + 10 and   // 左邊起漲超過十天且
   value3 > value4 * 1.1 then // 漲幅超過一成
begin
  value5 = linearregslope(high[1], period - value1 - 1);  // 算出最高點迄今的每根BAR最高價連線的斜率
  value6 = linearregslope(low[1], period - value1 - 1);  // 算出最高點迄今的每根BAR最低價連線的斜率

  if value5 < 0 and
     value6 < 0 and
     absvalue(value5 - value6) < 10 and  //兩條線的斜率都是負的且接近平行線
     (period - value1 - 1) > 5 and
     close[1] > close[2] and
     close > close[1] * 1.02 and
     volume > 1000 then
     ret = 1;
end;
```

## 參考資源

- [下降旗型且法人買超選股法](http://www.xq.com.tw/videoteach//videoteach/%e4%b8%8b%e9%99%8d%e6%97%97%e5%9e%8b%e4%b8%94%e6%b3%95%e4%ba%ba%e8%b2%b7%e8%b6%85%e9%81%b8%e8%82%a1%e6%b3%95/)
- [HighestBar - (系統函數)](https://xshelp.xq.com.tw/XSHelp/?HelpName=HighestBar&group=PRICERELFUNC)
- [下降旗形](https://wiki.mbalib.com/zh-tw/%E4%B8%8B%E9%99%8D%E6%97%97%E5%BD%A2)
