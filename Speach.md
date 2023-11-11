
<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B> Stock </B></summary>

當使用者選擇了顏色及尺寸之後，下方的Table view 會更新，顯示各個分店的/ 名稱/ 地址/ 電話及庫存數量。使用者可以透過這個功能，找到最近的分店，並且確認是否有庫存。如此一來就可以滿足消費者想要快速取貨，親自試穿等需求。

顏色與尺寸的選擇會使用 sample code 提供的UI，然後再去做判定，若兩者都有選擇，則會去後端抓取資料，並且更新table view。如果使用著只選擇顏色或是尺寸其中一個，則不會觸發判定機制。後端則會根據我們提供的資料，回傳各個分店的庫存數量。

#### (2 days)
- [x] Stock number fetched from backend
- [x] Table view to show branches info
- [x] Basic show stock number for each branches
</details>

---
<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Customer service</B></summary>
消費者可以在profile page選擇客服功能，當使用者對於商品的品質有疑慮時/ 需要退換貨時/ 對於服務態度有建議方向，可以透過這個功能，與客服人員進行即時的溝通。客服人員可以透過這個功能，即時的回覆使用者的問題，並且提供解決方案。

基本上進入聊天室後就跟line的聊天室差不多，做法則打算用table view 來呈現，並且使用stylish IQ keyboard，讓table view 跟著鍵盤一起往上推，不會被鍵盤擋住。


#### (2.5 day)
- [x] Profile page tableview
- [x] Textfield to send message
- [x] Send message to backend
- [x] Get message from backend
- [x] Use stylish IQ keyboard, to push table view.
- [x] Use Admin one on one chattting, without history.
</details>