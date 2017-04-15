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

## Hello World 逐词详解
在如下的代码段中，注意注释：
```swift
// `class` 是关键字，用于声明类；
// `Person` 是类的名字；
// `{` 表示一个 Scope 的开始。
class Person {

  // `var` 也是关键字，用于声明变量；
  // `name` 是变量名，这里省略了类型；
  // `=` 代表赋值，`""` 则是空字符串
  // 注意行尾不需要分号结尾
  var name = ""

  // `func` 是声明方法的关键字；
  // `sayHello` 是方法名字；
  // `(to: Person)` 是参数列表，
  // 其中 `to` 是参数名，`Person` 是参数类型
  func sayHello(to: Person) {
    // print 用于打印输出，括号中是参数；
    // 这里的参数构造了字符串，双引号中间的是字符串，
    // 反斜杠加括号 `\()` 可以将数据插入到字符串中。
    // 访问对象的属性用`点`操作，`to` 是对象，`name` 是属性。
    print("Hello \(to.name)")
  }
// `}` 表示 Scope 的结束。
// 大括号反应了包含关系：
//   Person 类包含一个 name、一个 sayHello，
//   sayHello 则包含了自己的实现（implementation）。
}

// 创建 Rose 变量，同样省略了类型。
// 创建对象通过构造器（或称 init 函数）
// Person 类没有声明构造器，系统会提供默认的无参构造器
// 调用任何方法，都需要括号：Person 是类型，Person() 才是调用
var rose = Person()
// 对变量的属性进行赋值
rose.name = "Rose"

// 创建 Jack 常量，`let` 表示常量
let jack = Person()
// jack 是常量，但是 jack 的属性是变量
// 对常量的属性进行赋值是可以的。
jack.name = "Jack"

// 访问对象的方法也是用`点`操作
// `to` 是参数名，对应于 Swift 的命名参数
// 同样，方法参数必须放到括号中
rose.sayHello(to: jack)

// 运行会输出：Hello Jack
// 注意 Swift 并不需要写 main 函数
// main 函数作为入口，可接收命令行参数，略
```

Hello world 中暗含了很多 **需要掌握的** 概念，清晰的概念有助于写出清晰的代码，上面提到的概念大概包括：
*常量、变量、类、方法、属性、scope、方法参数、方法调用、属性访问、方法访问、赋值、传参、命名参数、构造器、无参构造器、main 函数、命令行参数、…*

运行代码时也会接触到一些概念：*编译器、源码、二进制、交互式命令行、可执行文件、…*
