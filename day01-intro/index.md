# [Day01] 認識程式交易與 XScript

## 程式交易 v.s. 人為主觀交易

在股期權的交易市場上，只要一個風向改變，就是生存戰的開始。所以像專業投資人，除了要有一定的背景知識與經驗，還必須掌握各方資訊，並且即時出手，才能在戰場上存活下來。而業餘投資人不像是專業投資人般，有足夠精力和經驗可以嗅出戰前的哨聲，往往得先被廝殺一番，才能漸漸在市場中找到自己的生存之道。

對投資人來說，「紀律」是件很重要卻也很難做到的事。原因是我們幾乎無法以 100%的理性做決策，而且很容易將賭性的堅韌發揮在很有信心的事情上。因此，比起人為的主觀交易，「程式交易」是將投資人的進出場邏輯，轉換為給系統看得懂的策略語法，並機械式地執行交易。少了情感影響，投資人可以大幅避免一時衝動造成的損失 ; 而且條理化交易邏輯，也很好逐步改善，建立出適合自己的投資方式。

![程式交易的流程](https://i.imgur.com/tyfs893.png)

## 使用工具

目前實踐程式交易有兩種方式

- 自行開發：常見以 python、R 等程式語言自行撰寫交易程式，並且串接現有券商或交易所的資料。適合對程式語言相當熟悉、不習慣現有平台操作方式的人。
- 使用現有平台：目前主要有 XQ 系列軟體、MultiCharts 等桌面應用。投資人只需學習軟體的使用方式，就能進行程式交易。

![](https://www.xq.com.tw/images/xqlite_download_740_360.png)

## 誰適合做程式交易

答案是所有人！但是一定是程式交易至上嗎？這就不一定了。對於在主觀判斷上能維持高勝率的人，程式交易在他們的定位上就會是個決策輔助的角色 ; 但是相對於其他人，如果無法克服人性弱點，又無法花太多精神在這上面（像是每天沈浸在 flow coding 的 RD 們），程式交易就會是一個好選擇。

## 為什麼是 XScript

當然是因為要挺自家公司的產品啊（喂）  
學習 XScript 的好處有那些呢?

- 不須另外引進即時行情和設定下單 API 等細節，專注在實現交易的邏輯
- XScript 為台灣本土資訊商-嘉實資訊所研發的語法平台，針對市場需求不斷調整語法、新增功能
- 可讀性高，只要懂得基本程式邏輯(變數宣告、IF 判斷、迴圈、函式等)就能開始，對於工程師來說可以說是無痛上手
- 官方文件齊全，有時還會舉行課程。有關注粉絲專頁的人最近還會看到自己的大大手把手分享策略，可見用心(相關連結可以看底下參考資源)

其實 XScript 的資源已經算很豐富了，想認真自學的話是可以靠現有資源上手。不過如果你跟我一樣不知道從哪裡開始，或是還在觀望中的話，就可以跟著我一起慢慢探索 XScript 喔!

## 小結

相信在這裡看的 iT 人們，很多都跟我一樣，可能光是跟上工作的必修技術就分身乏術了。所以希望藉由這個系列，可以輕鬆入門程式交易，讓辛苦賺來的錢不用再繳學費，開始為自己加薪吧！

另外今年還有報名另外兩個主題，有興趣歡迎訂閱

- [從 ES 到 ESNext - 30 天輕鬆掌握 ECMAScript]()
- [前端工程師不能不知道的生產力工具]()

因為一天要寫三篇，為了確保文章品質，如果趕不及，可能就會先暫時停更這裡ＱＱ  
不過 YURI 還是會把這個系列完成喔!

## 參考資源

- [XScript 官方教學入口](https://www.xq.com.tw/School.aspx)
- [XQ 全球贏家粉絲專頁](https://www.facebook.com/XQ.com.tw/)
- [程式交易是什麼？能為我們帶來哪些好處？](https://www.pfcf.com.tw/software/detail/2174)