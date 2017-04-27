通常，判断多个对象不为空，我们使用如下代码：
```swift
var a: Int?
var b: Int?

// 一般语言的判断方式
if a != nil, b != nil {
  // a, b 仍然是 optional
  print(a, b)
}

// swift 的方式
if let a = a, let b = b {
  // a, b 都不是 optional
  print(a, b)
}
```

Swift 中，也可以用 switch 来做相同的事情：
```swift
var a: Int?
var b: Int?

switch (a, b) {
case let (l?, r?):
  // 注意问号
  // l, r 都不是 optional
  print(l, r)
default:
  break
}
```

但是这样是不可以的，会提示 * case will never be executed*：
```swift
switch (a, b) {
case let (l, r):
  // 因为这个 case 包含了剩下的情况
  print(l, r)
case let (l?, r?):
  print(l, r)
default:
  break
}
```

---
思路来源：在从 Swift 2.3 升级到 3.0 的过程中，xcode 有可能会生成如下代码：
```swift
// FIXME: comparison operators with optionals were removed from the Swift Standard Libary.
// Consider refactoring the code to use the non-optional operators.
fileprivate func < <T: Comparable>(lhs: T?, rhs: T?) -> Bool {
  switch (lhs, rhs) {
  case let (l?, r?):
    return l < r
  case (nil, _?):
    return true
  default:
    return false
  }
}

// FIXME: comparison operators with optionals were removed from the Swift Standard Libary.
// Consider refactoring the code to use the non-optional operators.
fileprivate func > <T: Comparable>(lhs: T?, rhs: T?) -> Bool {
  switch (lhs, rhs) {
  case let (l?, r?):
    return l > r
  default:
    return rhs < lhs
  }
}
```
