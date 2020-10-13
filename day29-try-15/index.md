# [Day29] 實戰 - 三關價偏多且 KDJ 維持多頭排列

## 影片在這裡

[![Yes](https://img.youtube.com/vi/5uLJGFFWsxY/0.jpg)](https://www.youtube.com/watch?v=5uLJGFFWsxY)

## 分類：`選股`

## 重點整理

-

## 程式碼

```javascript
var:up1(0),mp1(0),lp1(0);
up1=low+(high-low)*1.382;
mp1=(high+low)/2;
lp1=high-(high-low)*1.382;

if close > mp1 then ret=1;
```

## 參考資源

- [三關價偏多且 KDJ 維持多頭排列的交易策略](http://www.xq.com.tw/videoteach//videoteach/7794-2/)
