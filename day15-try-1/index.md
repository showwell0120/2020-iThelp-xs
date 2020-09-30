# [Day15] 實戰 - 多方勢力一起進場的股票

在官方網站的[實戰應用教學](http://www.xq.com.tw/videoteach/videolist.aspx)陸續都有新增公司大大分享的影片。每個單元時間也不長，大約 4~5 分。加上公司大大清楚的說明，其實很適合已經有點基礎的學習者觀看的影片喔。

經過前面的背景知識介紹，相信已經有些基本概念了。所以從今天開始到最後，我們直接以裡面的實戰應用來邊做邊學。Let's get start!

## 影片在這裡

[![Yes](https://img.youtube.com/vi/44dD7MQBqIg/0.jpg)](https://www.youtube.com/watch?v=44dD7MQBqIg)

## 分類：`指標` `選股`

## 重點整理

- 平常時候就能使用的選股法
- 找出投信、公司派、外資、市場主力等都在買的標的
- 執行腳本後出來的符合標的，盡量選擇中型股以上，並且才剛要開始漲的

## 程式碼

指標版本

```javascript
value1=GetField("關鍵券商買賣超張數","D");  // 大股東
value2=GetField("地緣券商買賣超張數","D");  // 專業經理人或小家券商
value3=GetField("綜合前十大券商買賣超張數","D");  // 觀察代操的進出
value4=GetField("外資買賣超","D");  // 三大法人
value5=GetField("投信買賣超","D");
value6=GetField("自營商自行買賣買賣超","D");
value7=GetField("主力買賣超張數","D");  // 非以上提到的市場主力

// 建立計數器，只有有欄位是呈現買超就加一
var:count(0);
count=0;
if value1>0 then count=count+1;
if value2>0 then count=count+1;
if value3>0 then count=count+1;
if value4>0 then count=count+1;
if value5>0 then count=count+1;
if value6>0 then count=count+1;
if value7>0 then count=count+1;

// 以上欄位的張數加起來除以成交量
value8=value1+value2+value3+value4+value5+value6+value7;
if volume<>0 then
  value9=value8/volume*100;

plot1(count,"參戰勢力數");  // 繪製各方的買超個數
plot2(value9,"佔交易比重"); // 繪製各方交易量佔全部交易量的比例
```

選股版本

```javascript
value1=GetField("關鍵券商買賣超張數","D");
value2=GetField("地緣券商買賣超張數","D");
value3=GetField("綜合前十大券商買賣超張數","D");
value4=GetField("外資買賣超","D");
value5=GetField("投信買賣超","D");
value6=GetField("自營商自行買賣買賣超","D");
value7=GetField("主力買賣超張數","D");

var:count(0);
count=0;
if value1>0 then count=count+1;
if value2>0 then count=count+1;
if value3>0 then count=count+1;
if value4>0 then count=count+1;
if value5>0 then count=count+1;
if value6>0 then count=count+1;
if value7>0 then count=count+1;

value8=value1+value2+value3+value4+value5+value6+value7;
value9=value8/volume*100;

// 建立條件是否成立的flag
condition1=false;
// 如果成交量超過2000張 且各方買超個數大於4 且各方交易量佔全部交易量的比例大於60
if volume>2000 and count>=4 and value9>60
  then condition1=true;

{
    barslast: 計算目前K棒與上次條件成立K棒的期數差
    回傳值為0表示條件成立當期，回傳值為1表示前1期條件成立，依此類推
}
if barslast(condition1)=0
  then ret=1;

outputfield(1,count,0,"符合條件數");
```

## 參考資源

- [各方勢力共襄盛舉的股票](http://www.xq.com.tw/videoteach//videoteach/%e5%90%84%e6%96%b9%e5%8b%a2%e5%8a%9b%e5%85%b1%e8%a5%84%e7%9b%9b%e8%88%89%e7%9a%84%e8%82%a1%e7%a5%a8/)
- [barslast](https://xshelp.xq.com.tw/XSHelp/?HelpName=BarsLast&group=DATERELFUNC)
