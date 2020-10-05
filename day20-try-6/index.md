# [Day20] 實戰 - Fscore 的選股法

## 影片在這裡

[![Yes](https://img.youtube.com/vi/2tr8GL9Xsuk/0.jpg)](https://www.youtube.com/watch?v=2tr8GL9Xsuk)

## 分類：`選股`

## 重點整理

- 財報公布後可使用的選股法
- Fscore 又稱皮爾托斯基分數(簡稱皮式分數)，由教授 Joseph Piotroski 提出
- 針對三大面向 - **獲利性**、**安全性**、**成長性**，各設定三個條件來為公司的營運狀況評分。分數愈接近 9，表示營運表現愈良好
- 獲利性三項條件：
  1. 當期資產報酬率(ROA) > 0  
     ※ `ROA = 稅後淨利 / 總資產` -> **運用資產賺錢的能力**
  2. 當期營業現金流 > 0
  3. 當期營業現金流大於淨利 -> 確保收入大多為本業獲利
- 安全性三項條件：
  1. 當期長期負債 < 上一期 -> 負債是否有減少
  2. 當期流動比例 > 上一期 -> 是否有營運危機
     ※ `流動比例 = 流動資產 / 流動負債` -> **以短期資產償還短期負債的能力**
  3. 上一期沒有發行新股
- 成長性三項條件：
  1. 當期 ROA > 上一期 ROA
  2. 當期毛利率 > 上一期 -> 成本控制的能力
  3. 當期資產週轉率 > 上一期
     ※ `資產週轉率 = 銷售收入 / 總資產` -> **營運效率**

## 程式碼

### Fscore 達到 9

```javascript
// 以季為腳本執行頻率
if barfreq<>"Q" then raiseruntimeerror("請改成用季頻率");

variable:count(0);
count=0; // 以計數器累加符合條件的分數

// 取得各條件所需欄位
value1=GetField("資產報酬率","Q");
value2=GetField("來自營運之現金流量","Q");
value3=GetField("本期稅後淨利","Q");
value4=GetField("長期負債","Q");
value5=GetField("流動比率","Q");
value6=GetField("加權平均股數","Q");
value7=GetField("資產報酬率","Q");
value8=GetField("營業毛利率","Q");
value9=GetField("總資產週轉率(次)","Q");
value10=GetFieldDate("營業毛利率","Q");

{
    獲利性：
    1. 當年度 ROA > 0
    2. 當年度的營業現金流 > 0
    3. 當年度的營業現金流大於淨利
}
if value1>0 then count=count+1;
if value2>0 then count=count+1;
if value2>value3 then count=count+1;

{
    安全性：
    4. 當年度長期負債金額小於上一年度
    5. 當年度流動比例(流動資產/流動負債)大於上一年度
    6. 上一年度沒有發行新股
}
if value4<value4[4] then count=count+1;
if value5>value5[4] then count=count+1;
if value6=value6[1] then count=count+1;

{
    成長性：
    7. 當年度的總資產報酬率大於上一個年度的總資產報酬率
    8. 當前毛利率大於上一年度
    9. 當前資產週轉率大於上一年度
}
if value7>value7[4] then count=count+1;
if value8>value8[4] then count=count+1;
if value9=value9[4] then count=count+1;

input: Fscorelimit(9); // 將分數輸入設為input
if count>=Fscorelimit then ret=1;

outputfield(1,count,0,"Fscoure");
outputfield(2,value10,0,"財報日期");
```

## 參考資源

- [Fscore 的選股法](http://www.xq.com.tw/videoteach//videoteach/fscore%e7%9a%84%e9%81%b8%e8%82%a1%e6%b3%95/)
- [F-Score 指標評分選股術，打敗八成投資人的秘訣](https://www.samchoulove.com/fscore-stock-picking/)
