# [Day19] 實戰 - 財報公佈後的轉機股大調查

## 影片在這裡

[![Yes](https://img.youtube.com/vi/2qiRWKxsw4k/0.jpg)](https://www.youtube.com/watch?v=2qiRWKxsw4k)

## 分類：`選股` `EPS` `本益比`

## 重點整理

- 財報公布後可使用的選股法
- 轉機股：滿足以下條件，表示公司的獲利可能開始恢復
  - 以過去 5 年的平均 EPS 計算，本益比偏低的話，表示前幾年過去獲利良好，但最近表現較差
  - 用最新一季的財報來看，獲利能力有明顯進步
- 可挑出值得長期關注的標的

## 程式碼

### 可能的轉機股

`GetFieldDate(欄位名稱, 頻率)`: 取得欄位的資料日期

```javascript
value1=(
    GetField("每股稅後淨利(元)","Y") +
    GetField("每股稅後淨利(元)","Y")[1] +
    GetField("每股稅後淨利(元)","Y")[2] +
    GetField("每股稅後淨利(元)","Y")[3] +
    GetField("每股稅後淨利(元)","Y")[4]
) / 5;  // 計算過去五年的每股平均稅後淨利


input:pehb(8,"本益比上限");  // 本益比上限抓8倍

if close < value1 * pehb then // 股價低於用過去五年平均EPS計算的八倍本益比
begin
    // 取各獲利能力相關的欄位季資料
    value2=GetField("營業毛利率","Q");
    value3=GetField("每股稅後淨利(元)","Q");
    value4=GetField("股東權益報酬率","Q");
    value5=GetFieldDate("營業毛利率","Q");
    if
      // 與上一季的資料相比
      value2 - value2[1] > 1 or
      value3 - value3[1] > 0.5 or
      value4 - value4[1] > 1
    then ret=1;
end;

// 增加選股結果的欄位
outputfield(1,value1,1,"過去五年平均EPS");
outputfield(2,close / value1,1,"本益比");
outputfield(3,value2 - value2[1],1,"毛利率季增加絕對值");
outputfield(4,value3 - value3[1],1,"EPS增加值");
outputfield(5,value4 - value4[1],1,"ROE增加值");
outputfield(6,value5,0,"財報日期");
```

## 參考資源

- [財報公佈後的轉機股大調查](http://www.xq.com.tw/videoteach//videoteach/%e8%b2%a1%e5%a0%b1%e5%85%ac%e4%bd%88%e5%be%8c%e7%9a%84%e8%bd%89%e6%a9%9f%e8%82%a1%e5%a4%a7%e8%aa%bf%e6%9f%a5/)
- [GetFieldDate - (內建函數)](https://xshelp.xq.com.tw/XSHelp/?HelpName=GetFieldDate&group=FIELDFUNC)
