# [Day18] 實戰 - 目標價的算法之一： 獲利穩定公司的目標價

## 影片在這裡

[![Yes](https://img.youtube.com/vi/Qq-VOSVZyWc/0.jpg)](https://www.youtube.com/watch?v=Qq-VOSVZyWc)

## 分類：`選股` `EPS`

## 重點整理

- 此選股策略適合獲利穩定的公司
- 先算出過去四季 **每股盈餘(EPS)** 的總和
- 如果是獲利穩定的公司，長期下來的 EPS 不會落差太大
- 以 **本益比 15 倍** 乘於最近五年來四季 EPS 的移動平均，算出目標價
- 如果收盤價距目標價差 2 成以上，則觸發條件成立

## 程式碼

### 獲利穩定股目標價計算方法

`summation(序列, 期數)`: 計算序列中前特定期數的資料總和。

`outputfield(輸出序號, 數值, 小數位個數, 輸出欄位名稱)`: 有需要在選股結果內輸出更多的欄位的話，則可以透過此函數來新增欄位。

- 輸出序號: 從 1 到 99，用來指定輸出欄位的順序
- 數值: 輸出的數值
- 小數位個數: 可不傳
- 輸出欄位名稱: 可不傳，預設為 **欄位 + 序號**

```javascript
value1 = getfield("每股稅後淨利(元)","Q");
value2 = summation(value1,4);  // 最近四季的EPS總和
value3 = highest(value2,20);  // 過去20季以來四季EPS總和的最高值
value4 = lowest(value2,20);  // 過去20季以來四季EPS總和的最低值
value5 = average(value2,20);

var:tp(0);// 建立目標價變數
if
  value4>1  // 連續4季合計的EPS在過去 20 季都大於 1 元
  and value3-value4<1.5  // 4季合計的EPS近20季以來最高與最低EPS差 1.5 元以內
then
  tp=15*value5;  // 本益比 15 乘於最近五年來4季 EPS 的移動平均

if close*1.2<tp then ret=1;  // 目標價與市價差20%以上

outputfield(1,tp,0,"目標價");
outputfield(2,(tp-close)/close*100,1,"預期報酬率");
```

## 參考資源

- [目標價的算法之一： 獲利穩定公司的目標價](http://www.xq.com.tw/videoteach//videoteach/%e7%9b%ae%e6%a8%99%e5%83%b9%e7%9a%84%e7%ae%97%e6%b3%95%e4%b9%8b%e4%b8%80%ef%bc%9a-%e7%8d%b2%e5%88%a9%e7%a9%a9%e5%ae%9a%e5%85%ac%e5%8f%b8%e7%9a%84%e7%9b%ae%e6%a8%99%e5%83%b9/)
- [OutputField - (內建函數)](https://xshelp.xq.com.tw/XSHelp/?HelpName=OutputField&group=GENERALFUNC)
- [Summation - (系統函數)](https://xshelp.xq.com.tw/XSHelp/?HelpName=Summation&group=PRICECULFUNC)
