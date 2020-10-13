# [Day28] 實戰 - 波段創新高

## 影片在這裡

[![Yes](https://img.youtube.com/vi/2us8MQp0nR0/0.jpg)](https://www.youtube.com/watch?v=2us8MQp0nR0)

## 分類：`選股` `波段`

## 重點整理

- 目的: 大盤或景氣表現不好時，價格還能創新高。表示背後有特別的原因
- 先找出符合以上描述的股票，再一檔一檔來研究。
  1. 找出波段最高點的一天 - highestdate
  2. highestdate 距離今天是幾根 K 棒
  3. 取得 highestdate 的收盤價
  4. 成交量超過 2000 張，且最近收盤價向上突破 highestdate 的收盤價，或是最近收盤價向上突破這段時間的最高價就觸發通知

## 程式碼

- `getbaroffset(日期)`: 依日期取得相對 K 棒位置

```javascript
input: highestdate(2020114), "請輸入波段最高點日期");
value1 = getbaroffset(highestdate);
value2 = close[value1];

if volume > 2000 then
begin
  if close cross over value2 or
     close cross over highest(high[1], value1) then
  ret=1;
  outputfield(1, value2, 1, "前一波指數高點收盤價");
  outputfield(2, value1, 0, "指數高點距今幾根bar");
end;
```

## 參考資源

- [如何挑選波段創新高的股票](http://www.xq.com.tw/videoteach//videoteach/%e5%a6%82%e4%bd%95%e6%8c%91%e9%81%b8%e6%b3%a2%e6%ae%b5%e5%89%b5%e6%96%b0%e9%ab%98%e7%9a%84%e8%82%a1%e7%a5%a8/)
- [GetBarOffset - (內建函數)](https://xshelp.xq.com.tw/XSHelp/?HelpName=GetBarOffset&group=GENERALFUNC)
