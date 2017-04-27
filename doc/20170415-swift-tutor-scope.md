# 作用域（Scope）
Scope 有范围的意思，如能力范围、活动范围。在编程中，主要指作用域。

作用域在很多语言中都是用大括号 `{}` 表示的，最常见的，类的定义、方法的定义：
```swift
class Person {
  // 类作用域开始

  var name = ""
  func sayHello(to: Person) {
    // 方法作用域
  }

  // 类作用域结束
}
```

---
# 作用域的嵌套
规则很简单：**内层可以访问外层**（让我们先忽略访问修饰符），如：
```swift
class Person {
  var name = ""
  func dump() {
    print(name) // 访问外层定义的 name
  }
}
```

Swift 等语言有全局作用域，内层访问外层仍然成立：
```swift
var personCount: Int = 0
class Person {
  init() {
    personCount += 1 // 访问全局定义的 personCount
  }
}
```

## 类型的嵌套
嵌套类型（Nested type）也可称为类型中的类型：
```swift
class Person {
  // Person 内部使用 Name
  var name = Name()

  // 定义一个嵌套类
  class Name {
    var firstName = ""
    var middleName = ""
    var lastName = ""
  }
}
// 外部使用 Name
var name1 = Person.Name()
```

内部类 `Person.Name` 和一般的类没有区别，除了名字长一点（*类似 java 中的静态内部类*），
带来的唯一限制是在 `Person` 外部使用时不能省略前缀。

嵌套类型带来的好处是清晰，**明确体现概念间的从属关系**，降低认知壁垒。

---
# 计算属性、扩展
## 计算属性（computed property）
它与普通的属性（stored property）是对应的，顾名思义，一个占据了存储空间，一个则是必须通过运算来求值：
```swift
class Rect {
  // 定义两个属性
  var width = 10
  var height = 20
  // 定义一个计算属性
  var area: Int {
    get { return width * height }
  }
}
```

注意几点：
- 也可以有 setter，如 `set(size) { ... }` 或 `set { ... }`
    - *若省略 `(size)`，参数名替换成 `newValue` 即可*
- 如果只有 getter，`get { }` 可以省略

## 扩展（extension）及使用扩展处理计算属性
为一个已有的类增加新功能，可以：
1. 传统OO的做法：继承这个类，引入新的类型
1. 修改这个类 —— 可能改变原有行为
1. 增加扩展 —— 已有的行为基本不变，也没有引入新的类型

前面的例子可以重写为：
```swift
class Rect {
  var width = 10
  var height = 20
}

// 在扩展中定义计算属性
extension Rect {
  var area: Int {
    get { return width * height }
  }
}
```

扩展没有改变已有类的行为，也没有引入新的类型，系统中很多内容也是通过扩展实现的。
使用扩展可以帮助我们 **分离关注点**。

## 结合作用域理解计算属性、扩展
规则只有一条，扩展是在 **原有作用域** 内增加的内容；扩展除了本身的目的（提供扩展功能），
还可以从物理上将代码分开：比如可将计算属性统一放到一个扩展中。逻辑上，类和扩展是属于同一个类的，相互访问没有限制。

## 举例：使用扩展重构已有代码
```swift
class Person {
  var aNnammeWithTypo = "Jack"
}

extension Person {
  var name: String {
    set { self.aNnammeWithTypo = newValue }
    get { return aNnammeWithTypo }
  }
}
```

---
# 静态成员
通常一个成员变量、方法是属于对象的，但如果用 `static` 或 `class` 修饰，那么它不属于任何一个对象。
静态的和全局的很像，区别仍然是名字：如全局的 `personCount` 和属于 Person 类的 `Person.personCount`。
我们应该避免定义全局的东西，**体现概念的从属关系**。

# 访问修饰符 / 访问控制
之前我们忽略了访问修饰符，**Swift 中没有包的概念，但是有模块（Module）的概念**，比如主程序就是一个模块，
第三方库也是以模块的方式体现的，访问修饰符就定义了模块内、模块间的访问控制：

|Swift 2.3|Swift 3|注释|
|:-:|:-:|-|
|-|open|写类库时用，使用者应该去继承它|
|public|public|写类库时常用，方便使用|
|internal|internal|默认值，模块内可访问|
|private|fileprivate|文件内可访问|
|-|private|所属作用域内可访问|

基于 **最小知识原则**，`private` 和 `fileprivate` 将是用的最多的，它是我们混乱不清的代码最后的遮羞布：
- `private` 成员只可以在声明的作用域内访问；
- `fileprivate` 则仅可以在文件内访问 —— Swift 其实是推荐使用扩展的。

---
# 在任意作用域内定义新的类型
类型嵌套，**符合直觉的做法就是类型套类型**，比如之前 `Person.Name` 的例子。

我们来举个例子以打破认知（*这个例子不用去记忆，看过即可*）：
```swift
func test() {
  // 在方法内部定义类型
  class Hell {
    var name = ""
  }
  var hell = Hell()
}
```

---
# 总结
- 大括号 `{}` 是作用域的精华，不需要质疑。
- 抛出一个问题：能不能把每个作用域都看做一个新的类型？
  - *可从类型是什么、何时开辟内存空间出发去思考*
