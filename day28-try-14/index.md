# [Day28] 實戰 - 盤中資金流向

## 影片在這裡

[![Yes](https://img.youtube.com/vi/c5E3_togC54/0.jpg)](https://www.youtube.com/watch?v=c5E3_togC54)

## 分類：`選股` `警示` `籌碼`

## 重點整理

-

## 程式碼

盤中警示

```javascript
value1=q_CashDirect;
value2=GetField("股本(億)","D")[1];
value3=GetField("投信買賣超張數")[1];
setbackbar(20);
input:length(20);
variable:up1(0);
up1 = bollingerband(value1, Length, 2 );
if
value2>10 and value2<40
and
 value1 crosses over up1
and close>close[1]
//量暴增而且股價上漲
and close<close[1]*1.05
//但漲幅沒有非常大
and value3>200
//投信前一日買超大於200張
then ret=1;
```

盤後選股

```javascript
value1=GetField("佔大盤成交量比","D");
value2=GetField("股本(億)","D");
value3=GetField("投信買賣超");
setbackbar(20);
input:length(20);
variable:up1(0);
up1 = bollingerband(value1, Length, 2 );
if
value2>10 and value2<40
and
 value1 crosses over up1
and close>close[1]
//量暴增而且股價上漲
and close<close[1]*1.05
//但漲幅沒有非常大
and value3>200
//投信前一日買超大於200張
then ret=1;
```

## 參考資源

- [盤中資金流向交易策略腳本](http://www.xq.com.tw/videoteach//videoteach/%e7%9b%a4%e4%b8%ad%e8%b3%87%e9%87%91%e6%b5%81%e5%90%91%e4%ba%a4%e6%98%93%e7%ad%96%e7%95%a5%e8%85%b3%e6%9c%ac/)
