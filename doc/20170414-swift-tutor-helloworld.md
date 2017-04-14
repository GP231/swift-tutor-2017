# Swift Hello World
Hello World 精髓在于真正写出来并执行，请确保你做得到。

环境配置很耗时，大约半天时间。

本文主要涉及：类、方法、属性

## Hello World
首先你需要一个目录用于放代码（如 `~/tmp/swift-tutor`）。
打开编辑器（如 Atom）输入如下代码，并保存为 `hello.swift`。
```swift
print("Hello World")
```

打开终端，用如下的命令运行
```sh
# 注意这是三条命令，且命令不包括美元符号
$ mkdir ~/tmp/swift-tutor
$ cd ~/tmp/swift-tutor
$ swift hello.swift
```

不出意外终端会打印 `Hello World`。

`swift` 命令如果不带参数，就会进入交互式命令行（`:help` 可查看帮助，`:exit` 或 `ctrl + D` 退出）：
```
$ swift
Welcome to Apple Swift version 3.0.2. Type :help for assistance.
  1>
```

`swiftc` 命令可生成可执行文件（或者称为二进制文件）。而且你应该已经注意到了，Swift 代码既可以直接执行，也可以生成二进制。

## 类
以 `Person` 举例：
```swift
// 声明一个类用 `class` 关键字
class Person {
  // 声明变量用 `var` 关键字
  var name = "Rose"
}
```

## 属性
重写 `Person` 类：
```swift
class Person {
  // name 的类型是 String
  var name: String = "Rose"
  let age: Int = 18
}
```

其中的 `var` 用于声明可变的属性（property）。不可变的则是用 `let`。注意，字段、成员变量、属性，都是同样的东西。

如果属性的类型可以推断，就可以省略。不能省略的情况如数字，Int、Double 等都可以是 `0`。

## 方法
`Person` 可以说你好，体现在代码中：
```swift
class Person {
  var name = "Rose"
  // 声明方法用 `func` 关键字
  func sayHello(to: Person) {
    print("Hello \(to.name)")
  }
}
```

## 综合例子
Rose 跟 Jack 说了 Hello：
```swift
class Person {
  var name = ""
  func sayHello(to: Person) {
    print("Hello \(to.name)")
  }
}

// 创建 Rose
var rose = Person()
rose.name = "Rose"

// 创建 Jack
var jack = Person()
jack.name = "Jack"

// 输出：Hello Jack
rose.sayHello(to: jack)
```

这些例子都很简单，但是一定要动手敲一遍，并能说出所有单词、符号的含义。
