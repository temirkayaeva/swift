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

### Простые значения

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

### Условия и циклы

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

