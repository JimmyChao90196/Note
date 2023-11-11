# Rules

### User chat
- user-check: 

```swift
socket.emit("user-check", ["userIdentify": ["user", "JWT"]])
```

---
- talk:

```swift
socket.emit("talk", ["userIdentify": ["user", "inputValue", "JWT"]])
```

---

### User chat
- user-check: 

```swift
socket.emit("user-check", ["userIdentify": ["admin", "JWT"]])
```

---
- talk:

```swift
socket.emit("talk", ["userIdentify": ["admin", "inputValue", "JWT"]])
```

---
- close:

```swift
socket.emit("user-close", ["userIdentify": ["admin", "JWT"]])
```