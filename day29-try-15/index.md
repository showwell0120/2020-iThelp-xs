# [Day29] 實戰 - 三關價偏多且 KDJ 維持多頭排列

## 影片在這裡

[![Yes](https://img.youtube.com/vi/5uLJGFFWsxY/0.jpg)](https://www.youtube.com/watch?v=5uLJGFFWsxY)

## 分類：`選股` `技術`

## 重點整理

- 三關價：今日振盪區間，可預測隔天的支撐壓力。公式如下 -
  1. 上關 = (昨日最高價 - 昨日最低價) \* 1.382 + 昨日最低價
  2. 中關 = (昨日最高價 + 昨日最低價) / 2
  3. 下關 = 昨日最高價 - ((昨日最高價 - 昨日最低價) \* 1.382)
     如果價格往中關以上突破，則適合做多操作; 跌破下關則做空操作; 在中關徘徊則是盤整階段。更多說明可以看[<三關價的應用>](https://blog.xuite.net/star297/starmoon/51592916-%E4%B8%89%E9%97%9C%E5%83%B9%E6%93%8D%E4%BD%9C%E7%AD%96%E7%95%A5+)的文章
- KDJ：中文叫隨機指標，運用一段時間內的收盤價、最高價、最低價，來衡量股價與正常範圍的變異程度。更多說明可以看[<3 分鐘認識 KDJ 指標>](https://histock.tw/blog/histock1688/193)的文章

## 程式碼

- 三關價偏多

```javascript
var:up1(0),mp1(0),lp1(0);
up1 = low+(high-low)*1.382;
mp1 = (high+low)/2;
lp1 = high-(high-low)*1.382;

if close > mp1 then ret=1;
```

- KDJ 維持多頭排列

`Stochastic(期數, K值平滑期數, D值平滑期數, 輸出RSV值, 輸出K值, 輸出D值)`：計算 KD 指標。可計算 KD 指標的 RSV、K 及 D 三個數值。Stochastic 函數回傳 1 時，代表計算成功。RSV、K 及 D 的值是回傳在第 4、5、6 個參數。

```javascript
input: Length(9, "天數"), RSVt(3, "RSVt權數"), Kt(3, "Kt權數");
var: rsv(0), k(0), d(0), days(0), j(0);

Stochastic(Length, RSVt, Kt, rsv, k, d);
j = 3 * d - 2 * k;

if k > 80 and _d > 40 and j > 20 then ret = 1;
```

## 參考資源

- [三關價偏多且 KDJ 維持多頭排列的交易策略](http://www.xq.com.tw/videoteach//videoteach/7794-2/)
- [三關價的應用](https://blog.xuite.net/star297/starmoon/51592916-%E4%B8%89%E9%97%9C%E5%83%B9%E6%93%8D%E4%BD%9C%E7%AD%96%E7%95%A5+)
- [3 分鐘認識 KDJ 指標](https://histock.tw/blog/histock1688/193)
