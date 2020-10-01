# [Day16] 實戰 - 本業有轉機且法人進場的選股策略

## 影片在這裡

[![Yes](https://img.youtube.com/vi/x2PEiXVs3pg/0.jpg)](https://www.youtube.com/watch?v=x2PEiXVs3pg)

## 分類：`選股`

## 重點整理

- 財報公布後可使用的選股法
- 先找出毛利率、營收利益創單季的新高，營運好轉的公司
- 再找出財報公布前後沒有明顯漲幅，並且找出法人開始進場的標的
- 實現完腳本後，還是得跑回測驗證是否可以拿來應用。不過這個腳本只鎖定在財報公布的特定期間，跑回測結果並沒有特別理想

## 程式碼

### 毛利率或營業利益單季創長期新高

`SetTotalBar`:指定腳本執行時的資料讀取筆數。

```javascript
settotalbar(28);  // 選取範圍為過去28季的資料

value1=GetField("營業毛利率","Q");
value2=GetField("營業利益","Q");
input:period(28,"過去N季");

if value1=highest(value1,period) // 如果過去一季的營業毛利率是過去28季的高點
or value2=highest(value2,period) // 或是過去一季的營業利益是過去28季的高點
then ret=1;  // 觸發警示通知
```

### 最近 N 日漲跌幅小於 M

`rateofchange(數列,期數)`: 已過去特定期數的 K 棒資料為基準點，計算至當期 K 棒的序列資料的變化率。
計算公式：( 當期價格 ／ N 期前價格 - 1 ) \* 100

```javascript
input:period(10,"計算區間");   // 設定計算區間
input:ratio(10,"最低漲跌幅");  // 設定最低漲跌幅

value1 = rateofchange(close,period-1);  // 計算過去的收盤價變化率
if value1 < ratio then ret=1;  // 如果變化率小於最低漲跌幅則觸發警示通知

outputfield(1,value1,1,"區間漲跌幅");
```

## 參考資源

- [本業有轉機且法人進場的選股策略](http://www.xq.com.tw/videoteach//videoteach/%e6%9c%ac%e6%a5%ad%e6%9c%89%e8%bd%89%e6%a9%9f%e4%b8%94%e6%b3%95%e4%ba%ba%e9%80%b2%e5%a0%b4%e7%9a%84%e9%81%b8%e8%82%a1%e7%ad%96%e7%95%a5/)
- [RateOfChange](https://xshelp.xq.com.tw/XSHelp/?HelpName=RateOfChange&group=PRICECULFUNC)
- [SetTotalBar](https://xshelp.xq.com.tw/XSHelp/?HelpName=SetTotalBar&group=GENERALFUNC)
