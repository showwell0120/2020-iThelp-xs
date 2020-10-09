# [Day25] 實戰 - 過去幾年配息超過一定標準

## 影片在這裡

[![Yes](https://img.youtube.com/vi/YjIYGYFSnzw/0.jpg)](https://www.youtube.com/watch?v=YjIYGYFSnzw)

## 分類：`選股` `存股`

## 重點整理

-

## 程式碼

```javascript
input:years(3,"最近N年");
input:limit1(20,"現金股利合計下限");
array:ValueArray[99](0);
var:i(0);
for i=1 to years begin
valuearray[i]=GetField("現金股利","Y")[i-1];
end;
value2=array_sum(valuearray,1,years);
//區間股利合計
if value2>=limit1 then ret=1;
outputfield(1,value2,1,"近幾年合計現金股利");
```

## 參考資源

- [找出過去幾年配息超過一定標準的股票](http://www.xq.com.tw/videoteach//videoteach/%e6%89%be%e5%87%ba%e9%81%8e%e5%8e%bb%e5%b9%be%e5%b9%b4%e9%85%8d%e6%81%af%e8%b6%85%e9%81%8e%e4%b8%80%e5%ae%9a%e6%a8%99%e6%ba%96%e7%9a%84%e8%82%a1%e7%a5%a8/)
