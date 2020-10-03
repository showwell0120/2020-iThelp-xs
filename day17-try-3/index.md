# [Day17] 實戰 - 預收款項選股法

## 影片在這裡

[![Yes](https://img.youtube.com/vi/Ddk7jfBbpUY/0.jpg)](https://www.youtube.com/watch?v=Ddk7jfBbpUY)

## 分類：`選股`

## 重點整理

- 以今周刊的[「洞悉合約負債 四步驟選出營收績優股」](https://www.businesstoday.com.tw/article/category/80401/post/201909040031/%E6%B4%9E%E6%82%89%E5%90%88%E7%B4%84%E8%B2%A0%E5%82%B5%20%20%E5%9B%9B%E6%AD%A5%E9%A9%9F%E9%81%B8%E5%87%BA%E7%87%9F%E6%94%B6%E7%B8%BE%E5%84%AA%E8%82%A1)的交易策略，作為腳本邏輯
- **合約負債**：有兩大科目 - 「預收工程款」跟「預收備料款」。公司預收從客戶給付的費用，並在期間內以商品或服務的形式提供給客戶。例如建商販賣預售屋、加入健身房繳交的年費等
- 如果預收款上增幅度大，可當作營收的領先指標
- 符合條件：本季預收款項比去年的同期成長 1.1 倍，且成長幅度超過股本的 20％
- 交易時機：成交價跟成交量都創 30 天的新高，但是漲幅跟 30 天來的低點來比小於 7％

## 程式碼

### 預收款項成長

```javascript
settotalbar(12);

input: ratio_1(1.1, "本季比去年同期增長N倍");
input: ratio_2(20, "預收款項成長佔股本X%");

// 計算過去四季預收款項成長的幅度佔股本比例
value1 = summation(GetField("預收款項", "Q"), 4);
value2 = summation(GetField("預收款項", "Q"), 4)[4];
value3 = value1 - value2;
value4 = value3 / (GetField("股本(億)","D") * 100);

if
GetField("預收款項", "Q") >= GetField("預收款項", "Q")[4] * ratio_1
and value4 > ratio_2 / 100 then
ret = 1;

outputfield(1, GetField("預收款項", "Q"), 2, "預收款項");
outputfield(3, GetField("預收款項", "Q")[4], 2, "去年同期預收款項");
outputfield(5, value4, 2, "預收款項成長佔股本比例");
```

### 爆量剛起漲

```javascript
//價量暴增但離低點不遠，這個跑日資料
input: period(30, "日期區間");
input: ratioLimit(7, "區間最大漲幅%");

if
close = highest(close, period) //今日最高創區間最高價
and volume = highest(volume, period) //今日成交量創區間最大量
and highest(high, period) < lowest(low, period) * (1 + ratioLimit * 0.01)
//今日最高價距離區間最低價漲幅尚不大
then
ret = 1;
```

## 參考資源

- [預收款交易策略](http://www.xq.com.tw/videoteach//videoteach/%e9%a0%90%e6%94%b6%e6%ac%be%e4%ba%a4%e6%98%93%e7%ad%96%e7%95%a5/)
