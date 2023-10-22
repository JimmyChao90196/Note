# How to manage third party frame work




<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Cocoa pod</B></summary>
We'll know how to install cocoapod and manage our third party framework.
If you don't, I recommand you go ahead and click the link below.

<br>

[How to install cocoa pod(Sean Allen)](https://youtu.be/MuMZZtQpB6Y?si=H5cUO1IPAf5Y4aDB)

He'll tell you how to install cocoa pod through terminal.


```
$ sudo gem install cocoapods
```
</details>
<br>

---
<details>
<summary style="font-size: 1.5em; color: #c89349"><B>Manage frameworks inside the project</B></summary>
Cocoa pod handle most of the heavy lifting for us so we can focusing on how to manage the libraries that comes with those handy framework.

<br>
<b>Method 1: Using extension</b><br>
By using extension, we are able to encapsulate and limit the scope of the framework.<br>
Also notice that we can also <span style="color: #c89349">wrap up functionalities</span> form those frameworks to better suit our needs.


```swift
extension UITableView {

    func addRefreshHeader(refreshingBlock: @escaping () -> Void) {
        mj_header = MJRefreshNormalHeader(refreshingBlock: refreshingBlock)
    }

    func endHeaderRefreshing() {
        mj_header?.endRefreshing()
    }

    func beginHeaderRefreshing() {
        mj_header?.beginRefreshing()
    }

    func addRefreshFooter(refreshingBlock: @escaping () -> Void) {
        mj_footer = MJRefreshAutoNormalFooter(refreshingBlock: refreshingBlock)
    }

    func endFooterRefreshing() {
        mj_footer?.endRefreshing()
    }

    func endWithNoMoreData() {
        mj_footer?.endRefreshingWithNoMoreData()
    }

    func resetNoMoreData() {
        mj_footer?.resetNoMoreData()
    }
}
```


<br>

---

<br>
<b>Method 2: Using custom class with singleton</b><br>
Or we can create a custom class for initializing the the functionality of the framework.
This way we don't have to initialize the whole things every time we try to use it.
I think it's an awesome and neat way to avoid creating repeatitive code.<br>
This method is basically an upgraded version of method 1. It takes a little bit more time to set up, but we can easily separate the framework logic from the view controller.



```swift
import JGProgressHUD

enum HUDType {
    case success(String)
    case failure(String)
}

class LKProgressHUD {

    static let shared = LKProgressHUD()

    private init() {}

    let hud = JGProgressHUD(style: .dark)

    var view: UIView {
        return AppDelegate.shared.window!.rootViewController!.view
    }

    static func show(type: HUDType) {
        switch type {
        case .success(let text):
            showSuccess(text: text)
        case .failure(let text):
            showFailure(text: text)
        }
    }

    static func showSuccess(text: String = "success") {
        if !Thread.isMainThread {
            DispatchQueue.main.async {
                showSuccess(text: text)
            }
            return
        }
        shared.hud.textLabel.text = text
        shared.hud.indicatorView = JGProgressHUDSuccessIndicatorView()
        shared.hud.show(in: shared.view)
        shared.hud.dismiss(afterDelay: 1.5)
    }

    static func showFailure(text: String = "Failure") {
        if !Thread.isMainThread {
            DispatchQueue.main.async {
                showFailure(text: text)
            }
            return
        }
        shared.hud.textLabel.text = text
        shared.hud.indicatorView = JGProgressHUDErrorIndicatorView()
        shared.hud.show(in: shared.view)
        shared.hud.dismiss(afterDelay: 1.5)
    }

    static func show() {
        if !Thread.isMainThread {
            DispatchQueue.main.async {
                show()
            }
            return
        }
        shared.hud.indicatorView = JGProgressHUDIndeterminateIndicatorView()
        shared.hud.textLabel.text = "Loading"
        shared.hud.show(in: shared.view)
    }

    static func dismiss() {
        if !Thread.isMainThread {
            DispatchQueue.main.async {
                dismiss()
            }
            return
        }
        shared.hud.dismiss()
    }
}
```
</details>




