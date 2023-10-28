# Access control in iOS dev



<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B> Introduction</B></summary>
 
 #### what is access control
Access control is a way to limit the code within a certain region.

 #### why do we need access control
We use access control to restrict the access of certain properties, methods, classes to the code from other source files and modules. This is useful when we want to hide the implementation details from the user, to prevent the original class from being contaminated by other code, or to prevent the user from messing with the implementation details.

#### Easier Debugging and Maintenance
When you limit the parts of the code that can interact with a particular piece of data or functionality, you reduce the areas you need to consider when debugging or refactoring.

當我們限制了某些class or function 並將其與其他 code 分離，也就減少人為疏失的機會，我們也可以更容易的debug and maintain the 這一整個project.

#### Independency
By limiting access, you can protect sensitive data and functions. While not a substitute for full-fledged security measures, proper access control is a line of defense against unauthorized or unintended activity.

我們可以想像一間大型公司的運作，每個部門都有自己的權限，這樣可以避免其他部門的人員干涉到不同部門的事務，整間公司就像是順利運行的生產線一樣，每個部門都有自己的工作，不會互相干涉。

#### Reduced Complexity
By hiding the internal complexities and exposing only what's necessary, you can make your code easier to read and understand, which is beneficial for both the original developers and any future developers who may work on the code.

使用access control 可以將需要呈現的特定功能暴露出來給使用者就好，而隱藏其他部分，這樣可以讓code更容易閱讀，也更容易理解。而且也能讓後續的開發者更容易閱讀和理解這段code。


</details>

---

<br>

<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Content</B></summary>

<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Access level and keywords [ v ]</B></summary>

### open
Open is the highest access level, which means the code can be accessed from anywhere, even from other modules. <br>

Let's forget about all the technical terms in UIKit or swift and imagine you<span style="color: #F8C471">(the class)</span> are holding a top secrete SCP foundation access key.

You can go from base 621 to base 300 with no problem. And you can even assign subordinate to other base. <br>

### public
Pulic access level is not as good as open, you are allowed to travel accross different base, exchange infromation from other base even. But that's it, you can do very little in other bases<span style="color: #F8C471">(as module in your project).</span>

### internal
If you are holding internal level key card, you can only access the base you are in. You can't go to other <span style="color: #F8c471">bases(as module in your app project)</span>, and you can't even exchange information with other bases. <br>

### fileprivate
If you are holding a file private level key card, you can only access a certain <span style="color: #F8c471">floor(as file in code)</span> in the base.

### private
private is the most protective access level, you can only access the <span style="color: #F8c471">room(as class in code)</span> you are in. You'er existence is completely unknown to others.

</details>


<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Simple example in code [ v ]</B></summary>

 #### Demonstrate the exmaple in code
</details>

<details>
<summary style="font-size: 1.2em; color: #F8C471"><B>Stylish case study and pratical application [ v ]</B></summary>

 
 
 #### When would you want to use fileprivate or private in class
 - When designing an HTTPClient class, 我們有用到 singleton 的概念，我們希望這個 class 只有一個 instance，所以我們把 init() 設為 private，這樣就可以避免其他人在這個class以外的地方外面亂用，而造成資料的混亂

  - StorageManager 也是類似的道理，如果一切的行為都交由 StorageManager 來處理，那麼我們就可以將所有關於 storage 的行為都寫在 StorageManager 裡面並且 mark as private，這樣就可以避免其他人在這個class以外的地方外面亂用，而造成資料的混亂

  - When implementing font extension，會用到輔助的function來存放程式片段，這些function只是給我們的 custom function 所使用的，並沒有必要讓其他人使用，所以我們可以將這些function mark as private，這樣就可以避免其他人在這個 UIFont 以外的地方使用！
  
 - 通常我們會比較常在framework的定義中看到 public and open，因為framework是給其他人使用的，所以我們會希望其他人可以使用這個framework中的class，但是我們又不希望其他人可以修改這個class，所以我們會使用public，而不是open，因為open可以被繼承，而public不行，這樣就可以避免其他人在這個class以外的地方外面亂用，而造成資料的混亂

</details>
 </details>

 ---

 <br>




<br><br>

<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Resources</B></summary>

[Brief explaination by Sean Allen ](https://youtu.be/RFGEzkBa834?si=aAhwdsjrD4daF7a2)

[Official swift documentation](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol/#)

[Popular article on medium](https://abhimuralidharan.medium.com/swift-3-0-1-access-control-9e71d641a56c)

[Hacking with swift](https://www.hackingwithswift.com/read/0/19/access-control)

[中文文章](https://itisjoe.gitbooks.io/swiftgo/content/ch2/access-control.html#)

[中文影片](https://www.youtube.com/watch?v=iyXuN5Df1rE)

</details>

---


