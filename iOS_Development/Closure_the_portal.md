# Closure - the easiest portal in swift


<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Portal use case in STYLiSH</B></summary>
<br>
The concept of closure is rather simple, it is a nameless function or snippet that can be passed around as a variable. What so special about it is that it can carray data with it. And we get to decide what to do with the data. But as for "when" to use it, that is decided by the class that owns the closure.<br><br>

Sounds familiar? Yes, it is very similar to delegate. But the difference is that delegate is a protocol, and it is a one to one relationship. But closure is a variable, and it can be passed around. So it is a one to many relationship. And it is more flexible than delegate.<br><br>

---

The code below shows that STTapPayViewController owns a closure, and what being carried out as an argument is a boolean value which indicates whether the card is valid or not. Now this information should be passed to CheckoutViewController, since it where we process most of the logic.
<br>

```swift
import UIKit
import TPDirect

class STTapPayViewController: STBaseViewController {

    // MARK: - @IBOutlet
    @IBOutlet weak var cardView: UIView!

    var cardStatusHandler: ((Bool) -> Void)?
    
    private var tpdCard: TPDCard!
    private var tpdForm: TPDForm!

    override func viewDidLoad() {
        super.viewDidLoad()

        // 1. Setup TPDForm With Your Customized CardView, Recommend(width:260, height:80)
        tpdForm = TPDForm.setup(withContainer: cardView)

        // 2. Setup TPDForm Text Color
        tpdForm.setErrorColor(.red)
        tpdForm.setOkColor(.blue)
        tpdForm.setNormalColor(.black)

        // 3. Setup TPDForm onFormUpdated Callback
        tpdForm.onFormUpdated { [weak self] status in
            // Use callback Get Status.
            self?.cardStatusHandler?(status.isCanGetPrime())
        }
    }
}
```
<br><br>
Since closure is actually reference type, the data that comes along with it can be passed to CheckoutViewController with no problem. And we can use the data to determine whether the user can proceed to the next step.
<br>


```swift
import UIKit

class CheckoutViewController: STBaseViewController {
    
    private struct Segue {
        static let success = "SegueSuccess"
    }
    
    @IBOutlet weak var tableView: UITableView!
    
    var orderProvider: OrderProvider! {
        didSet {
            guard orderProvider != nil else {
                tableView.dataSource = nil
                tableView.delegate = nil
                return
            }
            setupTableView()
        }
    }
    
    private lazy var tappayVC: STTapPayViewController = {
        guard
            let tappayVC = UIStoryboard.trolley.instantiateViewController(
                withIdentifier: STTapPayViewController.identifier
            ) as? STTapPayViewController
        else {
            fatalError()
        }
        addChild(tappayVC)
        tappayVC.loadViewIfNeeded()
        tappayVC.didMove(toParent: self)
        tappayVC.cardStatusHandler = { [weak self] flag in
            self?.isCanGetPrime = flag
        }
        return tappayVC
    }()

```
</details>

---






