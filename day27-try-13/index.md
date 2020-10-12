# [Day27] 實戰 - 撰寫均線金三角交叉的策略

## 影片在這裡

[![Yes](https://img.youtube.com/vi/HLRLTPGSJp8/0.jpg)](https://www.youtube.com/watch?v=HLRLTPGSJp8)

## 分類：`選股` `型態`

## 重點整理

- 金三角交叉：5 日均線先向上突破 10 日均線後再突破 20 日均線，10 日均線也向上突破 20 日均線，三條線的交叉處產生的三角形
  ![jpg](https://i1.kknews.cc/SIG=25urnil/2rr600039952835nr3r6.jpg)

## 程式碼

- `barslast(條件式)`: 計算目前 K 棒與上次條件成立 K 棒的期數差  
  回傳值為 0 表示條件成立當期，回傳值為 1 表示前 1 期條件成立，依此類推

- `cross over(序列, 期數)`:也可以寫成 **cross above**。檢查目前的欄位數值是否向上穿越某個欄位的前期數值。表示**黃金交叉**。

```javascript
value1 = barslast(average(close, 5) cross over average(close, 10));  // 五日均線與十日均線黃金交叉距今幾根bar

value2 = barslast(average(close, 5) cross over average(close, 20));  // 五日均線與20日均線黃金交叉距今幾根bar

if average(close, 10) cross over average(close, 20) and // 十日均線突破20日均線
   value1 < 7 and value2 < 7 and  // 五日均線在七天內分別突破十日與20日均線
   value1 > value2  // 且五日均線先突破十日均線再突破20日均線
then ret=1;
```

## 參考資源

- [如何撰寫均線金三角交叉的策略腳本](http://www.xq.com.tw/videoteach//videoteach/%e5%a6%82%e4%bd%95%e6%92%b0%e5%af%ab%e5%9d%87%e7%b7%9a%e9%87%91%e4%b8%89%e8%a7%92%e4%ba%a4%e5%8f%89%e7%9a%84%e7%ad%96%e7%95%a5%e8%85%b3%e6%9c%ac/)
- [barslast](https://xshelp.xq.com.tw/XSHelp/?HelpName=BarsLast&group=DATERELFUNC)
- [Cross Above / Cross Below](https://xshelp.xq.com.tw/XSHelp/?HelpName=Cross+Over&group=CONTROLFLOW)
- [Crossover 和 > 有什麼不同？](https://forum.xq.com.tw/thread/crossover-%E5%92%8C-%E6%9C%89%E4%BB%80%E9%BA%BC%E4%B8%8D%E5%90%8C/)
