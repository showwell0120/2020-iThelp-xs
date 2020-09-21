# [Day05] 輸出與流程控制

不管是寫哪種程式，其實都是試著把腦中所想的所有情境，轉換成系統可執行的語言。所以依照情況的不同，就會需要對應的控制機制，來幫助系統做出複雜的決策。接著就來看看 XS 中有那些相關語法吧！

## `if then else `

條件式的執行。而根據決策的複雜度，程式會有以下的流程組成
|程式結構|語意|
|---|---|
|`if` <條件> `then` <任務>;|如果符合<條件>，就執行任務|
|`if` <條件> `then` <任務 A> `else` <任務 B>;|如果符合<條件>，就執行<任務 A>。否則就執行<任務 B>|
|`if` <條件 1> `then` <任務 A> `else` `if` <條件 2> `then` <任務 B> ;|如果符合<條件 1>，就執行<任務 A>。否則如果符合<條件 2>，就執行<任務 B>|

試著練習看看吧!

```javascript
// 如果近一日漲幅為正，則發出警示通知
if close>close[1] then ret=1;

// ------------------------------

{
    如果昨日收盤價比今日最高價還高，那麼今日真實最高價就等於昨日收盤價
    否則今日真實最高價就等於今日最高價
}

if Close[1] > High then TrueHigh = Close[1]
else TrueHigh = High;

// ------------------------------

{
    如果開盤就漲停，則發出警示通知
    否則如果開盤跳空上漲後，不到九點十五分就漲停的話，也發出警示通知
}

if open=q_DailyUplimit then ret=1
else if open>close[1]*1.025 and close=q_DailyUplimit and time<091500
then ret=1;
```

在 coding style 上，一樣大小寫不區分，也可以在語法關鍵字換行。不過要注意的是，如果 `then` 後面還有 `else` 的流程判斷的話，就不要加上 `;`。

## `switch begin case end`

根據目標變數的值，來決定執行的程式區塊。

跟其他程式語言比較不一樣的地方是，因為 `switch case`絕大部分情況是多種 case，所以 XS 還需要多加兩個關鍵字來包覆多行的陳述式。

- `begin`: 在 `switch`之後，寫 `case` 之前
- `end`: 寫完 `case` 之後，表示各種數值選項的陳述式已結束

先來練習看看吧！

```javascript
variable:status(0)  // 使用 variable 建立status 變數
switch(close-close[1])
begin  // 開始數值選項的陳述式
case >0: status=1;
case <0: status=-1;
case 0: status=0;
end;  // 結束數值選項的陳述式
```

## 迴圈 (`for` / `while`)

跟其他的語言大同小異，有明確次數的重複執行，使用 `for`； 如果不確定次數的話，則以 `while` 加上判斷式來執行，直到判斷式回傳 false 為止。

for 迴圈的程式架構如下:  
`for` <數值 A> `to` <數值 B>  
`begin`  
 <執行指令 1>;  
 <執行指令 2>;  
 (...);
`end`

直接看看例子。

```javascript
variable:n(0), count(0);  // 使用variable建立 n 跟 count 變數
for n=1 to 5
begin
  if(high[n] > high[n-1]) // 如果當前的最高價大於前一時間單位的最高價
  then count=count+1;
end;
```

接著看看 `while` 怎麼寫  
`while` <判斷式>  
`begin`  
<執行指令 1>;  
<執行指令 2>;  
(...);  
`end`

看個範例程式

```javascript
sumValue=0;
while i<5  //直到 i 的數值 >= 5時才會停止
  begin
    sumValue=sumValue+close[i]; //累加前i期的收盤價
    i=i+1;  // 每次執行時加1
  end
avgValue=sumValue/5; //SumValue為近5期收盤價的加總，avgValue為近5期平均收盤價
```

## `begin end`

這兩個關鍵字是一個組合關鍵字，只要是有多行的陳述式需要執行時，就需要用這兩個關鍵字把陳述式包覆。最常使用在流程控制裡，執行指令的地方。

以一張大大做的範例說明圖來看看

![IMG](http://cdn.xstrader.net/wp-content/uploads/2015/10/%E5%A4%9A%E6%A2%9D%E4%BB%B6%E5%A4%9A%E6%95%98%E8%BF%B0%E7%B0%A1%E5%96%AE%E6%A8%A1%E5%BC%8Fsample.png)

這段程式的意思是

- 如果開盤就漲停，就執行敘述式群 A
- 在敘述式群 A 中，如果過去十根 K 棒漲幅都沒有超過 2.5%就觸發，就觸發警示通知
- 如果沒有開盤漲停，但開高後在 9:15 之前就漲停，就執行敘述式群 B
- 在敘述式群 B 中，如果過去十天漲幅不到兩成，就觸發警示通知

## 小結

今天介紹的部分，對於實現高複雜度的策略有很大的幫助，大家也可以先試著練習看看喔。

今天就到這邊  
Happy trading ! 明天見囉 !

## 參考資源

- [if..then](http://xstrader.net/if-then/)
- [switch case](http://xstrader.net/switch-case/)
- [begin..end](http://xstrader.net/begin-end/)
- [迴圈](http://xstrader.net/%E8%BF%B4%E5%9C%88/)
