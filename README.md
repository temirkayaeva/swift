Swift — мультипарадигменный объектно-ориентированный язык программирования, созданный компанией Apple для разработчиков iOS и OS X. Swift работает с фреймворками Cocoa и Cocoa Touch и совместим с основной кодовой базой Apple, написанной на Objective-C. Swift задумывался как более безопасный язык в сравнении с Objective-C. Язык поддерживается в среде программирования Xcode 6; программы на нем компилируются при помощи Apple LLVM и используют рантайм Objective-C, что делает возможным использование обоих языков (а также pure С и С++) в рамках одной программы. Был анонсирован на конференции разработчиков WWDC 2014.


Swift исключает большой пласт распространенных программных ошибок при помощи применения современных программных паттернов:

* Переменные всегда инициализированы до того, как будут использованы.
* Индексы массивов всегда проверяются на out-of-bounds ошибки.
* Целые числа проверяются на переполнение.
* Опционалы гарантируют, что значения nil будут явно обработаны.
* Автоматическое управление памятью
* Обработка ошибок позволяет осуществлять контролируемое восстановление от непредвиденных ошибок.

# Основы языка Swift

Традиционно, рассказ о новом языке начинается с Hello, world! В Swift это делается так:

```swift
println("Hello, world!")
```

## Простые значения

 let  используется для создания констант и var  - для объявления переменных. Значение константы не обязательно должно быть известно на момент компиляции, но оно должно присваиваться строго один раз. Это значит, что можно использовать константу для обозначения значения, определяемого единажды, но используемого во многих местах.
 
 ```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

Константа или переменная должна иметь тот тип, что и значение, которое хотите присвоить ей, однако не обязательно всегда объявлять тип — компилятор сам может определить тип, если при создании константы или переменной указывается ее значение. В приведенном выше примере, компилятор определит, что myVariable — это целое число (integer), т.к. начальное значение — целое число.

Если начальное значение не предоставляет достаточной информации (или его нет), тип указывается вручную:

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

Значения никогда не конвертируются в другой тип неявно. Если необходимо сконвертировать значение в другой тип, то нужно показать это явно: 

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

Есть еще один простой способ поместить значение в строку. 

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "U have \(apples + oranges) pieces of fruit."
```

Массивы и словари создаются с помощью квадратных скобок ([]), а получить доступ к их значениям можно указав индекс или ключ в квадратных скобках. 

```swift
var shoppingList = ["catfish", "water", "tulips"]
shoppingList[1] = "bottle of water"
 
var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

Массив автоматически увеличивается при добавлении элементов.

```swift
shoppingList.append("blue paint")
print(shoppingList)
```

Чтобы создать пустой массив или словарь, используется синтаксис инициализации:

```swift
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

## Условия и циклы

Для создания условий используются операторы **if**  и **switch**, для создания циклов – **for-in**, **for**, **while** и **do-while**. При этом выделять круглыми скобками условия и инициализирующие выражения необязательно, тогда как фигурные скобки обязательны.


```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
teamScore
```

Условие внутри оператора if должно быть логическим, это в частности означает, что выражение if score {…} является ошибочным, поскольку здесь нет явного сравнения (например, с нулем).

Условный оператор *if* можно использовать совместно с *let* и *var* для работы с константами и переменными, которые могут иметь значение *nil*. Такие константы и переменные называются **опциональными**. Чтобы создать опциональную переменную или константу добавьте знак вопроса (?) после указания типа.

```swift
 var optionalString: String? = "Hello"
optionalString == nil
 
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

Если опциональное значение равно *nil*, условие будет ложным и код в фигурных скобках после *if* выполнен не будет. В противном случае переменной *greeting* будет присвоено новое значение.

### switch

Оператор множественного выбора *switch* поддерживает внутри себя множество других операторов сравнения и не ограничен лишь простыми сравнениями:

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    let vegetableComment = "Add some raisins and make ants on a log."
case "cucumber", "watercress":
    let vegetableComment = "That would make a good tea sandwich."
case let x where x.hasSuffix("pepper"):
    let vegetableComment = "Is it a spicy \(x)?"
default:
    let vegetableComment = "Everything tastes good in soup."
}
```

После выполнения подходящего блока кода, программа покидает оператор *switch*, не проверяя последующие условия. Таким образом вам не нужно вручную добавлять операторы прерывания *(break)* в конце каждого блока *case*.

### for-in

Для перебирания элементов ассоциативного массива используйте оператор *for-in* совместно с указанием пары имен для каждой пары ключ-значение.

```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
largest
```

### while 

Оператор цикла *while* позволяет выполнять блок кода внутри него до тех пор, пока условие не станет ложным. Условие также может быть указано после блока, который в таком случае будет выполнен по крайней мере один раз.

```swift
var n = 2
while n < 100 {
    n = n * 2
}
n
 
var m = 2
do {
    m = m * 2
} while m < 100
m
```

### for  

Оператор for можно использовать для перебора последовательности чисел с помощью двух точек (..) или с помощью инициализатора, условия и инкремента. 

```swift
var firstForLoop = 0
for i in 0..3 {
    firstForLoop += i
}
firstForLoop
 
var secondForLoop = 0
for var i = 0; i < 3; ++i {
    secondForLoop += 1
}
secondForLoop
```

## Функции и замыкания

Для объявления функций используйте ключевое слово *func*. Вызов функции производится через указание ее имени и списка аргументов в круглых скобках. Возвращаемый тип следует отделить от перечня формальных аргументов с помощью ->.

```swift
func greet(name: String, day: String) -> String {
    return "Hello \(name), today is \(day)."
}
greet("Bob", "Tuesday")
```

Функции также могут иметь неопределенное число аргументов:

```swift
func sumOf(numbers: Int...) -> Int {
    var sum = 0
    for number in numbers {
        sum += number
    }
    return sum
}
sumOf()
sumOf(42, 597, 12)
```

Функции являются объектами первого класса *(first-class type)*, иными словами, функция в качестве свого результата может возвращать другую функцию.

```swift
func makeIncrementer() -> (Int -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

Функция также может принимать другую функцию в качестве одного из аргументов.

```swift
func hasAnyMatches(list: Int[], condition: Int -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(numbers, lessThanTen)
```

**Функции являются частным случаем замыканий**. Вы можете создать замыкание, не указывая его имени и окружив тело замыкания фигурными скобками ({}). Для отделения аргументов и типа возвращаемого значения от тела замыкания используйте оператор *in*.

```swift
numbers.map({
    (number: Int) -> Int in
    let result = 3 * number
    return result
    })
```




