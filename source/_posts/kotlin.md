# Hello World
```
fun printHello(){
    println("hello world")
}
```

# 基础
## 变量定义
* var : 值可以改变
* val : 值不可以改变  相当于final

## 基本数据类型
* Int
* Long
* Double
* Float

### 运算
```
 + - * / 分别代表 加减乘除 
```
**特殊用法:**   
数据类型后接函数调用：
```
eg:

2.plus(3)
2.times(3)
3.div(5)

```
### 类型转换
```
val b2: Byte = 1 // OK, literals are checked statically
println(b2)
⇒ 1

val i4: Int = b2.toInt() // OK!
println(i4)
⇒ 1

val i5: String = b2.toString()
println(i5)
⇒ 1

val i6: Double = b2.toDouble()
println(i6)
⇒ 1.0

```
### 数字中的下划线
Kotlin允许使用下划线来分割一个较长的数字，为了代码的可读性。
```
val oneMillion = 1_000_000
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```

## 字符串
### 格式化
```
val numberOfFish = 5
val numberOfPlants = 12

var str = "I have $numberOfFish fish" + " and $numberOfPlants plants"

var str2 = "I have ${numberOfFish + numberOfPlants} fish and plants"

```
## if/else
### 通用写法
```
val numberOfFish = 50
val numberOfPlants = 23
if (numberOfFish > numberOfPlants) {
    println("Good ratio!") 
} else {
    println("Unhealthy ratio")
}
```
### 高级用法
#### 区间
```
val fish = 50
if (fish in 1..100) {
    println(fish)
}
```
#### 多重选择
```
when (numberOfFish) {
    0  -> println("Empty tank")
    in 1..39 -> println("Got fish!")
    else -> println("That's a lot of fish!")
}
```
等同于
```
if (numberOfFish == 0) {
    println("Empty tank")
} else if (numberOfFish < 40) {
    println("Got fish!")
} else {
    println("That's a lot of fish!")
}
```

## 关于null
变量默认不能为null，如
```
var rocks: Int = null
```
如果想强制设置为null，则应该使用:
```
var marbles:Int?=null
```
判断变量是否为空
```
var fishFoodTreats = 6
if (fishFoodTreats != null) {
    fishFoodTreats = fishFoodTreats.dec()
}
```
特殊用法: 
```
var fishFoodTreats = 6
fishFoodTreats = fishFoodTreats?.dec()
fishFoodTreats = fishFoodTreats?.dec() ?: 0
```
强制抛出NullException
```
val len = s!!.length   // throws NullPointerException if s is null
```

## 数组和列表
### list
定义一个不可改变的list
```
val school = listOf("mackerel", "trout", "halibut")
println(school)
```
定义一个可以改变的list，以及删除其中一项
```
val myList = mutableListOf("tuna", "salmon", "shark")
myList.remove("shark")
```
### Array
定义一个普通的array
```
val school = arrayOf("shark", "salmon", "minnow")
println(java.util.Arrays.toString(school))
```
array中可以拥有不用类型
```
val mix = arrayOf("fish", 2)
```

# 函数
## main函数
```
fun printHello() {
    println ("Hello World")
}

printHello()
```
## 一切皆value

表达式的执行结果可以作为值放在表达式的右侧

```
val isUnit = println("This is an expression")
println(isUnit)
```
```
val temperature = 10
val isHot = if (temperature > 50) true else false
println(isHot)
```
```
val temperature = 10
val message = "The water temperature is ${ if (temperature > 50) "too warm" else "OK" }."
println(message)
```

## when 用法
kotlin中的when类似于java的switch，具体如下：
```
fun fishFood (day : String) : String {
    return when (day) {
        "Monday" -> "flakes"
        "Wednesday" -> "redworms"
        "Thursday" -> "granules"
        "Friday" -> "mosquitoes"
        "Sunday" -> "plankton"
        else -> "nothing"
    }
}

```

## 函数参数默认值
类似于C++, kotlin中可以定义一个函数参数中的默认值
```
fun swim(speed: String = "fast") {
   println("swimming $speed")
}

swim()   // uses default speed
swim("slow")   // positional argument
swim(speed="turtle-like")   // named parameter
```
当有多个参数需要指定默认值时
```
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20): Boolean {
    return when {
        temperature > 30 -> true
        dirty > 30 -> true
        day == "Sunday" ->  true
        else -> false
    }
}
```
 
# 类
## 创建类
Eg:
```
pacakge example.myapp
class Aquarium{
    var width: Int = 20
    var height: Int = 40
}
```
默认类型的属性可以直接方位如:
```
myAquarium.width = 10
```

## 添加成员函数
```
fun printSize(){
    println("hello world")
}
```
## 添加构造函数
构造函数不需要在类体内定义一个函数，而是直接可以将构造函数写在类的右边。如：
```
class Aquarium( length: Int = 100 , width: Int = 20 , height: Int = 40){
    var length: Int = lengh
    var width: Int = width
    var height: Int = height
...
}
```
以上更简便的写法是可以直接指定将构造函数参数变为成员变量, 通过使用var关键字:
```
class Aquarium( var length: Int = 100 ,vat width: Int = 20 ,var height: Int = 40){
...
}
```
## init函数
可以在类中加入若干个init块并依次执行.
```
class Aquarium (var length: Int = 100, var width: Int = 20, var height: Int = 40) {
    init {
        println("aquarium initializing")
    }
    init {
        // 1 liter = 1000 cm^3
        println("Volume: ${width * length * height / 1000} l")
    }
}
```
## 二级构造函数
一个kotlin类可以拥有除了构造函数和init函数之外的二级构造函数。二级构造函数使用关键字 constructor
```
    constructor(numberOfFish: Int) : this() {
        // 2,000 cm^3 per fish + extra room so water doesn't spill
        val tank = numberOfFish * 2000 * 1.1
    }
```
## 添加setter和getter
将一个属性设置setter和getter，可以在获取和赋值时自动调用。
```
var volume: Int
    get() = width * height * length / 1000
    set(value) {
        height = (value * 1000) / (width * length)
    }
```
## 可见性修饰符
* public : 外部可访问，是每个属性默认的类型。
* internal : 一个module范围内可以访问。
* private: 只有类内部可以访问。
* protected: 类内部和子类可以访问。

## 属性的部分可见性
如果一个属性想区分读和写的两个权限,可以单独对 setter 和 getter 做private 修饰,
```
    var volume: Int
        get() = width * height * length / 1000
        private set(value) {
            height = (value * 1000) / (width * length)
        }
```
## 类的继承
默认情况下，类不能被继承，同样的属性和方法也不能被子类重写。如想继承需要添加**open**关键字:
```
open class Aquarium (open var length: Int = 100, open var width: Int = 20, open var height: Int = 40) {
    open var volume: Int
        get() = width * height * length / 1000
        set(value) {
            height = (value * 1000) / (width * length)
        }
```