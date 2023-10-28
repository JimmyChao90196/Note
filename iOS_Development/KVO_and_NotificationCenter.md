# KVO and Notification center


<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>KOV in stylish</B></summary>
To properly set up KOV, we need to set up the following things - <br>
In the class that we want to observe it's property<span style="color: #c89349">( In this case StorageManager )</span>:<br><br>

- Decide a property to be observed<br>
- The class that owns this property should be the subclass of NSObject<br>
- This property should be marked as @objc dynamic<br>
<br>

```swift
    @objc dynamic var orders: [LSOrder] = []
```

Then in the class that we want to be notified<span style="color: #c89349">( In this case TrolleyViewController)</span>:<br>

- Set up the observer<br>
- Assign key path to the observer<br>
- Set the additional options to better suit our needs<br>
- Inside the change handler, we can get a new value each time the value changes<br>

By doing so, we can not only get values at the beginning, but also get notified when the value changes. So ~ pretty cool!
 <br>

 ```swift
     private var observation: NSKeyValueObservation?
 ```
 ```swift
     private func fetchData() {
        observation = StorageManager.shared.observe(
            \.orders,
            options: [.initial, .new],
            changeHandler: { [weak self] (_, value) in
                guard let datas = value.newValue else { return }
                self?.orders = datas
            }
        )
    }
 ```
 <br>

 ---

<details>
<summary style="font-size: 1.25em; color: #229954"><B>Pros</B></summary>

- It's synchronous, so the observer will be notified right after the value changes.<br>
- No need for posting notifiecation, it'll automatically notified when the value changes.<br>
 
</details>

<details>
<summary style="font-size: 1.25em; color: #E74C3C"><B>Cons</B></summary>

- Unless the class that owns the property is a subclass of NSObject, we can't use KOV.<br>
- Unless the class that owns the property is a singleton, we'll have to own the instance of that class.<br>
- It's not as flexible as Notification Center, it's a little verbose to set up.<br>
</details>
</details>
<br>

---


<details>
<summary style="font-size: 1.5em; color: #c1ac40"><B>Notification center in my SYLiSH</B></summary>

<details>
<summary style="font-size: 1.25em; color: #85C1E9"><B>Setup broadcaster</B></summary>
To properly set up a notification, we need to set up the following things - <br>
In the class that we want to broadcast the changes<span style="color: #c89349">( In this case StorageManager )</span>:<br><br>

- Setup a notification name <span style="color: #3498DB">(Like setting up frequency for the radio)</span><br>
- Post the notification with the name we just set up <span style="color: #3498DB">(Like broadcasting the radio)</span><br>

Now we are all setkup as a qualified broadcaster~<br>
```swift
//MARK: - Define notification name -
extension Notification.Name{
    static let stylishTokenDidGetNotify = Notification.Name("stylishTokenDidGetNotify")
}
```
```swift
//MARK: - Additional function
extension TabBarController{
    
    func passData(token: String, data: ProfileData) async throws{
        
        guard let nvcs = self.viewControllers else{ print("nvcs found nil"); return }
        
        for nvc in nvcs{
            guard let nvc = nvc as? UINavigationController else{ print("nvc found nil"); return }
            
            if let vc = nvc.viewControllers.first as? CartViewController{
                vc.token = token
                NotificationCenter.default.post(name: .stylishTokenDidGetNotify, object: token) }
            
            if let vc = nvc.viewControllers.first as? ProfileViewController{
                vc.profileData = data
            }
        }
    }
}
```
<br>

---
</details>



<details>
<summary style="font-size: 1.25em; color: #3498DB"><B>Setup listener</B></summary>
In the class that we want to get notified the changes<span style="color: #c89349">( In this case CheckoutViewController)</span>:<br>

- Setup a listener so we can recieve the notification we just setup<span style="color: #3498DB">(Like setting up a radio and tuning to the right frequency)</span><br>
- Setup a @objc function to perform custom action when the notification is recieved
<br><br>

```swift
//Listener
NotificationCenter.default.addObserver(self, selector: #selector(getToken), name: NSNotification.Name("stylishTokenDidGetNotify"), object: nil)
```

```swift
//MARK: - Notification action
extension CheckoutViewController{
    @objc func getToken(notification: NSNotification){
        if let token = notification.object as? String{
            self.token = token
        }
    }
}
```
<br>

---
</details>




<details>
<summary style="font-size: 1.25em; color: #229954"><B>Pros</B></summary>

- Broadcasters and listeners don't need to have reference to each other, so it's more flexible.<br>
- Notification center is one to many, so we can have multiple listeners for one broadcaster.<br>
 
</details>

<details>
<summary style="font-size: 1.25em; color: #E74C3C"><B>Cons</B></summary>

- It's asynchronous, so the listener will not always be notified right after the value changes.<br>
- When there's mulitple posting and listening event going on in your app. It can be very hard to maintain.<br>
- We have to manually posting the event, so it's not as convenient as KOV.<br>

</details>
</details>
<br>

---











