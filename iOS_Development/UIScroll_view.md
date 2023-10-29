# UIKit Scroll in iOS Development

<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Introduction</B></summary>

#### What is UIKit Scroll
#### Why is Scrolling Important in iOS

大家好，今天我們要來談談一個很酷的東西－－UIScrollView。你可以把 UIScrollView 想像成一個比螢幕還大的畫布。比如說，你有一篇很長的文章或一張大圖片，顯然它們是不可能完全適合你的 iPhone 螢幕的，對吧？UIScrollView 讓你能在這個大畫布上移動。讓我們既可以平移也可以縮放，so~ pretty cool, right?

但最厲害的是，UIScrollView 不只是一個獨立的角色，它還是 UITableView 和 UICollectionView 的superclass。是的，你在設定應用程式中滾動的tableView或者相冊中的collectionView，全部都是建立在 UIScrollView 上的！所以，了解 UIScrollView 就像是了解UITableView and UICollectionView的底層是如何運作的。這對於創建動態的iOS User interface 來說是基本的。這就是它如此重要的原因！
</details>

---

<br>

<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Content</B></summary>

<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Content Inset [ v ]</B></summary>

#### What is content inset
#### When do we use it

Alright，還記得我們談過的 UIScrollView 吧，就是那個讓你窺視更大圖片的大窗口。有時候你會想給這個圖片一點呼吸的空間，對吧？這就是 'Content Inset' 出場的時候。把它想成是在你的內容周圍添加一些額外的 padding，就像給你的內容一個舒適的靠墊！
當你有一個 navigation bar 或 tab bar 之類的東西時，你不想讓你的內容被它們遮住，對吧？Content inset 來救援！你可以調整頂部、底部、左側或右側的 insets 來給予額外的空間。

</details>

<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Content Offset [ v ]</B></summary>

#### What is content offset
#### When do we use it
Okay folks, let's talk about 'Content Offset'. Content offset 其實就是content view 與原點的位移差。

假設你正在閱讀一篇長文章，你已經讀到一半了。當你關閉應用程式並稍後回來時，你不會想從頂部開始，對吧？你會希望從你上次離開的地方繼續。這就是 content offset 派上用場的地方。它會記住你上次的滾動位置。
還有另一個酷炫的用例：視差滾動！你有沒有見過那些花俏的應用程式，在你滾動時，背景比前景移動得慢？那都是通過操縱 content offset 完成的。
所以總而言之，Content Offset 是關於控制和記住你在 scroll view 中的位置(個人比較習慣用位移差來解釋)。無論是用於閱讀應用程式、照片庫，還是一些花俏的動畫，玩弄 content offset 可以帶來更佳的使用者體驗。
</details>


<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Content Layout Guide [ v ]</B></summary>

#### What is Content Layout Guide
#### When to use it
</details>
Now, let's talk about 'Content Layout Guide' 的東西。這基本上是你在 scroll view 裡面使用 Auto Layout 時的最佳夥伴。你知道，在一個 scroll view 裡，你可能有各種東西，可能是文字、圖片、按鈕，等等。你如何確保一切都整齊地布置好呢？這就是 Content Layout Guide 的用武之地。

你有沒有在應用程式中建立過一個表單，其中有一些字段需要特定的位置？你知道，這裡是名稱字段，那裡是密碼，也許底部有一個不錯的小按鈕。Content Layout Guide 可以幫助你輕鬆地做到這一點。
或者，你有沒有看過那些應用程式裡酷炫的分步教程？你可以向左或向右滑動以查看不同的步驟。Content Layout Guide 就是確保每一個 'step'的圖片都完美地放置的。So yeah, it's a pretty essential tool for building a dynamic iOS user interface.



<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Frame Layout Guide [ v ]</B></summary>

#### What is Frame Layout Guide
#### When to use it
</details>
Frame Layout Guide 幫助我們定義 scroll view 的可見區域。It's like a frame to a picture.

例如，假設你有一些浮動按鈕或標題，你希望它們在用戶滾動時保持固定。Frame Layout Guide 是確保這些元素不會走失的你的首選。
你有沒有使用過一個應用程式，在頂部有一個不會在你滾動時移動的 sticky header？ Yeah，那就是 Frame Layout Guide doing it's job。它確保這樣的元素無論用戶滾動多少都保持固定和可見。

<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>UIScrollViewDelegate Methods [ v ]</B></summary>

#### scrollViewDidScroll(_ scrollView: UIScrollView)
The name is pretty self explainatory. When the view is scrolling, this method will be called.

例如，假設你正在創建一個閱讀應用程式，並且你希望在用戶向下滾動以閱讀更多內容時隱藏導航欄－－scrollViewDidScroll 就是你的人選。一旦用戶開始滾動，這個方法就會被觸發，然後你可以添加你的代碼來隱藏導航欄。
The prespective trick we just talked about，其中背景以比內容不同的速度移動。每次 scrollViewDidScroll 被調用時，你都可以調整 content size to achieve this effect.
Also, if we want to limit the scrolling direction, we can use this method to achieve that as well.
Long story short，scrollViewDidScroll 為你提供了關於滾動事件的實時更新。

#### scrollViewDidEndDecelerating(_ scrollView: UIScrollView)
好，所以你已經用所有酷炫的滾動功能吸引了用戶的注意，但當滾動停止時會發生什麼呢？這就是 scrollViewDidEndDecelerating 和 scrollViewDidEndDragging 方法的用武之地。將這些方法想像為電影拍攝中的 'Cut!' 命令。
當我們需要知道scroll view 目前停下來的內容時，我們可以使用 scrollViewDidEndDecelerating 來做到這一點。例如，假設你正在創建一個應用程式，其中有一個圖片輪播器。你想要在用戶停止滾動時知道他們正在查看哪張圖片。這就是 scrollViewDidEndDecelerating 的用武之地。

#### viewForZooming(_ scrollView: UIScrollView)
The name is pretty self explainatory. When the view is zooming, this method will be called.

假設你有一個圖像庫，並希望用戶能夠放大特定圖像。你會在 viewForZooming(in:) 中指定該圖像。 可以搭配 scrollViewDidEndDecelerating 來找出目前使用只想要放大的圖像。
或者，也許你有一個地圖視圖，並希望用戶能夠放大到特定位置。也可以使用 viewForZooming(in:) 來做到這一點。

<br>
</details>


</details>

---

<br>

<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Case Studies</B></summary>

<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Simple Demo</B></summary>

- Use delegate to limit the scrolling direction
- Use delegate and content offset to calculate page index
- Use delegate to zoom in and out the image

- Demonstrate content inset.
- Demonstrate content size.

- Scroll View will be able to dictate whether you wanted to scroll or interacte the content within scroll view.

</details>

<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Stylish Scenarios</B></summary>

- Demonstrate how scroll view calculate the current page index.
- Demonstrate how to snap to page.
</details>




</details>

---

<br>

<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Conclusion</B></summary>

#### Summary of UIKit Scroll Features
好的，各位，這結束了我們對 UIKit 的 UIScrollView 的深入探討！從基本的內容如 content inset 和 offset，到驅動滾動和縮放的細緻delegation method，我們涵蓋了很多。記住，UIScrollView 是其他 UIKit element，如 UITableView 和 UICollectionView 的支柱，所以精通它是至關重要的。無論你是設計一個照片庫，一個閱讀應用程式，還是一個複雜的地圖界面，UIScrollView 都能夠被使用到。感謝大家的捧場，and happy coding!
</details>

---

<br>

<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>References</B></summary>

[中文文章](https://medium.com/@leeningthebest/uiscrollview-786e3a6d0c00)
[彼得文章](https://medium.com/彼得潘的-swift-ios-app-開發問題解答集/scroll-view-決定捲動範圍的-content-layout-guide-6f606740918a)

[OfficialDoc_ScrollView](https://developer.apple.com/documentation/uikit/uiscrollview)

[OfficialDoc_ScrollViewDelegate](https://developer.apple.com/documentation/uikit/uiscrollviewdelegate)

[OfficialDoc_ContentLayoutGuide](https://developer.apple.com/documentation/uikit/uiscrollview/2865870-contentlayoutguide)

[OfficialDoc_FrameLayoutGuide](https://developer.apple.com/documentation/uikit/uiscrollview/2865772-framelayoutguide)

[YoutubeVideo](https://www.youtube.com/watch?v=YA20F7RJnwA)

</details>
