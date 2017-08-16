*[原文地址](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html#//apple_ref/doc/uid/TP40014097-CH2-ID1)*
# Swift 之旅
一般来说，用一个新的编程语言来编程的第一步是在屏幕上打印出一句 “Hello,world!”。Swift 是这样做的。

```
print("Hello,world!")
```
如果你有写过 C 或者 Objective-C 语言的话，那这种语法应该对你来说很熟悉。在 Swift 中，这段代码是一个完整的程序，它不需要引入别的库，也不需要你做字符串拼接处理。写在全局域内（*全局域可以大致理解为写在方法外的代码）的代码会被当做程序的入口，所以你不在需要 main() 这样的入口函数。而且你不需要在每一句代码后增加分号。

这篇文字通过展示如何完成各种各样的编程任务来向你介绍 Swift.如果你不理解内容中一些引用的代码，不要担心，这本书的剩余部分会更详尽的为你讲解。

## 简单的值
使用 `let` 来声明一个常量，使用 `var` 来声明一个变量。常量在编译时可以不赋值，但是它只能被赋值一次。这就说明你可以用常量来定义一个只赋值一次，但在很多地方使用的值。

```
var myVariable = 42
myVariable = 50
let myConstant = 42
```
你想给一个变量或者一个常量赋值的内容的类型必须是一样的，但是你不必要为他们每次都声明类型，因为当你再初始化时赋值编译器会为你推断出它的类型。在上面的代码例子中因为 `70` 是整数类型所以编译器推测出 `myvariable` 这个变量是一个整数类型的变量。

如果初始值没有提供足够的信息（或者没有初始值），可以在变量后明确写出这个变量的类型，用冒号分开。

```
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

Swift 的变量或者常量不可以包含多个类型，如果你需要将一个值转为别的类型，可以在变量前明确类型名称。

```
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```


在字符串中插入变量，可以在将变量写在 “\” 后，例子如下：
```
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

使用三个双引号可以创建一个多行的文本。文本从 3 个双引号开始到下一个 3 个双引号结束。下面是例子：

```
let quotation = """
Even though there's whitespace to the left,
the actual lines aren't indented.
Except for this line.
Double quotes (") can appear without being escaped.
 
I still have \(apples + oranges) pieces of fruit.
"""
```

使用方括号([])来创建一个数组或者字典，可以通过在方括号中写数字序号或者字典的键来访问每一个元素。最后一个元素的末尾也可以写一个逗号。


```
var shoppingList = ["catfish", "water", "tulips", "blue paint"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechnic",
]
occupations["Jayne"] = "Public Relations"
```

可以用初始化语法去创建一个空的数组或者字典。

```
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

当你设置一个新的变量或者给一个函数传递参数时，如果这个值的类型可以被推断出，就可以利用 [] 或者 [:] 建立一个空的数组或者字典。


```
shoppingList = []
occupations = [:]
```

## 控制流
使用 ``if`` 和 ``switch`` 建立一个条件语句，使用 ``for-in`` 、``while``、``repeat-while`` 建立一个循环语句。条件或循环变量的圆括号是可以省略的但是条件体或者循环体的花括号是不能省略的。


```
let individualScores = [75,43,103,87,12]
var teamScore = 0
for score in individualScores{
    if score > 50{
        teamScore += 3
    } else {
        teamScore += 1;
    }
}
print(teamScore)
```

在 ``if`` 语句中，条件语句必须是一个布尔值得表达式，就是说像 ``if score{... } `` 是错误的，而不是将 ``score`` 和 0 比较。

一个可以为空的值等于一个值或者等于一个空值（nil）。一个值得类型后面写一个问号(?)表面它这个值是可以为空的。你可以对一个可能为空的值 ``if`` 和 ``let`` 一起用。入下：


```
var optionalString: String? = "Hello"
print(optionalName: == nil)

var optionalName: String? = "John Appleseed"
var greeting = "Hello?"
if let name = optionalName {
    greeting = Hello,\(name)"
}
```

如果可以为空的值是空的话，条件判断就是语句就是失败，大括号中的代码就不会执行。如果这个可以为空的值被解包并且赋值到了 ``let`` 后的常量，那么大括号中的代码就能能到这个被解包后的值。

另一种处理可以为空的值得方法是利用 ``??`` 操作符给可空值提供一个默认值。如果可空值为空的话它的值就会变为默认值。如下：


```
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)"
```

``switches`` 语句提供了多种类型数据的比较操作，不在仅限于整数和判断是否相等。如下：

```
let vegetable = "red pepper"
switch vegetable = {
case "celery"
    print("Add some raisins and make ants on a log.")
case "cucumber","watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
```

需要注意的是在这里在每一个 ``case`` 语句中 ``let`` 关键词是如何将值复制给一个常量的。

如果 ``switch`` 语句成功匹配到了其中的一个 ``case`` ，执行完这个 ``case`` 中的代码后，程序就会退出这个 ``switch`` 语句。程序不会执行这个 ``case`` 后的下一个 ``case`` ，所以就不需要在没有个``case`` 语句后添加 ``break``。

你可以通过提供一对键值对的名字并利用 ``for-in`` 循环语句去遍历一个字典中的元素。因为字典是一个无序集合，所以它的键值对遍历是一个无序的遍历。如下：

```
let interestingNumber = [
    "Prime": [2,3,5,7,11,13],
    "Fibonacci": [1,1,2,3,5,8],
    "Square": [1,4,9,16,25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
```

使用  ``while`` 语句可以重复执行一个代码块直到条件判断改变。条件判断可以放在语句放在最后，但是需要保证这个循环最少能执行一次。

```
var n = 2
while n < 100 {
    n *=2
}
print(n)

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
```

你可以使用 ``.<`` 来表示一个区间。如下

```
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
```

使用 ``..<`` 是一个左闭右开区间，``...``表示一个闭区间。

## 方法和代码块
用 ``func`` 关键字可以声明一个方法。调用一个方法需要在方法名后面加上用小括号包着的参数列表和参数类型。使用 ``->`` 分开参数列表和返回值类型。如下：

```
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person)
```

在默认情况下方法的调用参数名(argument label)就是它的参数名(parameter name)。在声明方法时参数名前可以自定义调用参数名，如果不需要调用参数名可以写一个 ``_``。

```
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

可以使用元组来声明一个混合类型的集合，例如一个方法的返回值是多个值，就可以返回一个元组。元组的每一个元素可以通过序号或者名称访问到。例子如下：

```
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0
    
    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }
    
    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
print(statistics.2)
```

函数是可以嵌套的。被嵌套的方法可以访问到嵌套它方法的外方法。你可以利用嵌套的函数来管理和组织复杂冗长的代码。例子如下：

```
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

函数是第一等级的对象。函数的返回值可以是另一个函数。例子如下：

```
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

一个函数可以当做另一个函数的参数。例子如下：

```
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return ture
        }
    }
    return false
}
func lessThanTen(number: Int) -> Boll {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

一个代码块就是一个可以是一段稍后执行的代码，而函数其实是特殊形式的代码块。一个代码块可以访问到它在创建时所在域的变量和函数，即使在另一个域执行也依然可以访问到，上面的嵌套函数的即使例子。你可以使用 ``({})`` 来声明一个没有名字的代码块，使用 ``in`` 关键字来分开函数主体和参数返回值。

```
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

有几种方法可以让你写的代码块更简洁。当一个代码块的类型是已知的（比如代码块是一个代理的回调方法），那么你就可以省略掉代码块的参数类型或者返回值类型，或者两者都省略掉。只有一个语句的代码块返回的就是这一个语句的值。例子如下：

```
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
```

你可以使用参数序号去访问参数代替是用名字访问参数，这个方法在端的代码块中非常必要。如果一个代码块被当做一个函数的最后一个参数，那么它就可以直接写在小括号的后面。如果一个代码块是一个函数调用时用到的唯一参数，那么你可以省略掉小括号。


## 对象和类
在 ``class`` 关键词后面加上自定义的类名就是创建了一个类。在一个类中声明一个属性的格式和声明一个常量或者变量的方式是一样的，除了这个属性是在这个类的上下文中。类的方法的函数的声明也是一样的。例子如下：

```
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

使用类名加小括号去创建一个类的实例化对象。使用点语法可以访问对象的属性和方法。例子如下：

```
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

上面这个版本的 ``shape`` 类丢掉了一个重要的内容：一个初始化器。使用 ``init`` 可以创建一个

```
class NamedShape {
    var numberOfSides: Int = 0
    var name :String
    
    init(name: String) {
        self.name = name
    }
    
    func simpleDescription() -> String {
        return "Ashape with \(numberOfSides) sides."
    }
}
```

子类重写父类的方法需要在方法前加 ``override`` 关键字。如果重写父类方法不加 ``override`` 时会报错。写了 ``override`` 但是不是父类拥有的方法也会报错。

```
class Square: NamedShape {
    var sideLength: Double
    
    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }
    
    func area() -> Double {
        return sideLength * sideLength
    }
    
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

类的属性除了可以存储变量还可以生成 ``getter`` 和 ``setter``.

```
class EquilteralTriangle: NameShape {
    var sideLength: Double = 0.0
    
    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }
    
    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }
    
    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)"
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
triangle.perimeter = 9.9
print(triangle.sideLength)
```

在 ``set`` 方法中如果 ``newValue`` 表示设置的新值，也可以在在 ``set`` 关键词后的括号内自定义关键字。

需要注意的是 ``EquilateralTriangle`` 类的这个初始化器有三个不同的步骤。1、设置当前类声明的属性的值。2、调用当前类的初始化器。3、更改父类初始化器设置的属性值。其他的一些需要的设置也可以在这一步完成。

如果你需要在 ``set`` 方法执行前和执行后做以下操作可以使用 ``willSet`` & ``didSel`` 。这些你写在 ``willSet`` & ``didSel`` 中的代码，只要属性的值在初始化器之外更改就会执行。举个例子，下面的类会保证三角形的边长将用户按与正方形的边长相等。


```
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        square.sideLength = newValue.sideLength
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValuew.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
print(triangleAndSquare.triangle.sideLength)
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangeleAndSquare.triangle.sideLength)
```

你可以在方法、属性、下标公式前写一个 ``?`` 来表面它是一个可变的值。如果这个 ``?`` 前的值是 ``nil`` 那么 ``?`` 后面的代码都不会执行，而且这个语句的值会为 ``nil``。如果可为空值解包成功的话，所有 ``?`` 后的程序会按解包后的值运行。在这两种情况下，整个语句的值都是一个可为空的值。

### 枚举和结构体
使用 ``enum`` 关键字可以创建一个枚举。枚举和类可以养，可以有方法和它关联。例子如下：

```
enum Rank Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
    func simpleDescription() -> String {
        switch self {
            case .ace: 
                return "ace"
            case .jack:
                return "jack"
            case .queen:
                return "queen"
            case .king:
                return "king"
            default:
                return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

在默认情况下，Swift 用 0 开始对每一行赋值并且以每次加一的方式递增。你也可以使用明确的值去给每一行赋值。在上面的例子中， ``Ace`` 给定了明确的值 ``1`` ，那么下面的每一张的值就会以加一的方式递增。你也可以使用字符串或者浮点类型的数给枚举的每一行赋值。使用枚举类型的 ``rowValue`` 属性可以访问到枚举的每一个类型的值。

使用 ``init?(rawValue:)`` 可以初始化一个枚举类型的对象。它返回一个匹配这个值得枚举类型对象，或者 ``nil``。例子如下：

```
if let couvertRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

枚举的每一行的类型名称都是一个真实的值，而不是行值的另一种书写方式。事实上，如果枚举的每一行没有一个有意义的值，那么你就不需要给他提供一个。

```
enum Suit {
    case spades, hearts, diamond, clubs
    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```

注意上面的两种枚举类型的书写方式：当给 ``hearts`` 常量赋值时，``Suit.hearts`` 使用全名的方式表示，因为它没有一个明确的类型。在 ``switch`` 语句中，每一个 ``case`` 是以缩写的的形式表示，如 ``.hearts`` ，因为 ``self`` 的类型是已知的。你可以在已知枚举类型名称的任意时候使用缩写形式来书写。


如果一个枚举是有行值的，（就是行值是枚举声明的一部分）那么每一个行值的实例对象都有相对的行值。枚举的另一种呈现方式是没有行值得，枚举每一行的值是在枚举实例化时赋值的，这样的枚举不同的对象有不一样的行值。这种枚举的类型叫做关联值枚举类型，你可以把这种枚举类型当做存储属性的枚举类型的实例。举个例子，向服务器请求日出和日落时间，返回结果如果是正确的话那么就告知日出和日落时间，如果请求失败返回错误的话就是放回一个错误的提示。代码实现如下：

```
    enum ServerResponse {
        case result (String, String)
        case failure (String)
    }
    
    let success = ServerResponse.result("6:00", "8:09")
    let failure = ServerResponse.failure(out of cheese.")
    
    switch success {
    
        case let .result(sunrise, sunset):
            print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
        case let .failure(message):
            print("Failure... \(message)")
    }
```

这里需要注意的是日出和日落时间是如何从服务器返回值中提出出来然后然后和和 ``switch`` 语句的每一种情况做对比的。

用 ``struct`` 可以创建一个结构体。结构体提供了和类一样很多功能比如方法和初始化器。类与结构体之间最大的不同是，结构体在赋值时是传递赋值了一份，而类则是传递引用。

```
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription())) of \(suit.simpleDescription())"
    }
}
let threeOfSpades =. Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription() 
```

### 协议和扩展
使用 ``protocol`` 关键字声明一个协议。

```
protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust {}
}
```

类、枚举和结构体都可以声明协议。

```
class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty: Int = 69105
    func adjust() {
        simpleDescription += " Now100% adjusted."
    }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "A simple strucure"
    mutating func adjust() {
        simpleDescription += " (adjused)"
    }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

在结构体的方法中使用 ``mutating`` 修饰的方法可以修改本身。而在类的内部，方法不必使用 ``mutating`` 关键字，因为类的方法本来就可以修改自己。

使用 ``extension`` 关键字可以扩展一个已知的存在的类型，比如增加方法或者属性。你可以对一个任意一个类型进行扩展，包括引入工程的。

```
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)
```

你可以向使用其他类型一样来使用协议，比如创建一个对象集合，他们是不同的类型但是同时遵守一个协议。如果你使用一个协议类型的对象那么，这个协议外定义的方法是无法使用的。

```
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
```

一般使用一个遵循 ``Error`` 协议的类型来表示一个错误。

```
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```

使用 ``throw`` 可以抛出一个错误。使用 ``throws`` 关键字可以表示一个方式拥有抛出一个错误的能力。如果一个方法抛出错误，那么这个方法会立刻返回然后处理错误的代码会被执行。

```
func send(job:Int, toPrinter printerName: String) throw -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```
有下面几种处理错误的方法。一种是是用 ``do-catch`` : ``try`` 关键字后面的代码可以抛出异常。在 ``catch`` 代码块中，错误会以 ``error`` 的名字给出，你可以自定义它。

```
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)
}
```

你可以写多个 ``catch`` 代码块去处理不同的错误类型。你在 ``catch`` 后面写的代码的样式和在 ``switch-case`` 后面的写的样式是一样的。

```
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerError.onFire)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("printer error: \(printerError).")
} catch {
    print(error)
}
```

另一种方式是使用 ``try?``关键字把结果改变为一个可为空值。如果一个方法抛出异常，具体的异常将被忽略然后返回一个空值。如果没有抛出异常，那么返回一个包含返回值的可空值。

```
let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
```

使用 ``defer`` 声明一个代码块，代码块中的代码会在方法内其他所有代码执行完成后（返回前）执行。代码块中的代码不管发放是否抛出异常都会执行。使用了 ``defer`` 关键字使得把设置和清空的代码放在一块，还保证了他们在不同的时候运行。

### 泛型
在尖括号中写一个方法名或者类型名可以声明一个泛型。

```
func make Array<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result = [item]()
    for _ in 0..<numberOfTimes {
        result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```

方法、类、枚举和结构体都可以使用泛型结构。

```
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```

在方法实现前加 ``where`` 关键字可以明确指出满足哪些条件才能执行。举个例子，需要实现一个协议，需要两个类型是相同的，需要一个类型有一个指定的父类。代码如下:

```
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs:T, _ rhs: U) -> Bool 
    where T.Iterator.Element: Equatable, T.Iterator.Element == U.Iterator.Element {
        for rhsItem in rhs {
            if lhsItem == rhsitem {
                return ture
            }
        }
        return false
    }
    anyCommonElements([1,2,3], [3])
```

写 ``<T: Equatable>`` 和写 ``<T> ... where T: Equatable`` 的效果是相同的。






