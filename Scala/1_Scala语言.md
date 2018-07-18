# 1. main:

```js
object HelloWorld {
   def main(args: Array[String]) {
      println("Hello, world!")
   }
}
```

# 2.  变量常量:

```js
val s1 = "string" //常量
var s2 = "string" //变量(有初始值,无需类型)
var i1 = 1

var i1 : Int      //变量(无初始值,声明类型)
var s1 : String
```

# 3. 包和引用包:

```js
package com.jxg
import java.awt.Color
import java.awt._ //引入包下所有成员

class MYClass{

}
```


# 4. 数据类型:

```js
Byte Short Int Long Float Double Char String Boolean  Null
Unit //void
Nothing //最子类
Any //最超类
AnyRef  //引用(reference class)最基类
```


# 5. 元组:

```js
//1. 声明
val (i1,s1) = Pair(40,"string")
val t = (1, 3.1415 , "name")

//2. 调用
t._1
```


# 6. 修饰符

```js
//默认为public

//方法
private def myMethod(){
  println("f")
}
```

# 7. 内部类

```js
class Outer{
    class Inner{
    }
}
```

# 8. new

```js
(new MyClass).myMethod()
```

# 9. for和break

```js
// for 循环
var a = 0;
for( a <- 1 to (myList.length - 1)){
   println( "Value:" + myList(i));
}

// forin 循环
for ( x <- myList ) {
   println( x )
}

// Breaks 循环
val loop = new Breaks;
loop.breakable{
    for(...){
       ....
       loop.break;// 循环中断
   }
}
```

# 10. 方法
```js
//声明
object add{
   def addInt( a:Int, b:Int ) : Int = {
      return a + b
   }
}

//调用
object Test {
   def main(args: Array[String]) {
        println( "Returned Value : " + addInt(5,7) );
   }
}
```

# 11. 闭包

```js
//匿名方法
object Test {
   def main(args: Array[String]) {
      println( "value = " +  multiplier(1) )
      println( "value = " +  multiplier(2) )
   }
   val multiplier = (i:Int) => i * 3
}
```

# 12. 字符串

```js
//1. 字符串合并
var s1 = "string1"
var s2 = "string2"
var s3 = s1.concat(s2)

//2. 字符串格式化
var floatVar = 12.456
var intVar = 2000
var stringVar = "insertString"
var fs = printf("浮点型变量为 %f, 整型变量为 %d, 字符串为 %s", floatVar, intVar, stringVar)
```

# 13. 数组

```js
//1. 声明
var z = new Array[String](3)
var z = Array("Runoob", "Baidu", "Google")

//2. 合并
var myList1 = Array(1.9, 2.9, 3.4, 3.5)
var myList2 = Array(8.9, 7.9, 0.4, 1.5)
var myList3 =  concat( myList1, myList2)

//3. 声明区间数组
var myList2 = range(10,20)
```

# 14. 集合List

```js
//1. 声明
val nums1 : List[Int] = List(1, 2, 3, 4)
val nums2 = 1 :: (2 :: (3 :: (4 :: Nil)))

//2. 合并
var nums3 = List.concat(nums1,nums2)
```

# 15. 集合Set

```js
import scala.collection.mutable.Set

val set1 = Set(1,2,3)
set.add(4)
set.remove(1)
set += 5
set -= 2

```

# 16. Map

```js
import scala.collection.mutable.Map //可变map时,引入

var A : Map[Char,Int] = Map()
val colors = Map("red" -> "#FFFFFF", "blue" -> "#FFFFFF")

```

# 17. Option

```js
val myMap: Map[String, String] = Map("key1" -> "value1")
val value1: Option[String] = myMap.get("key1") //为value1
val value2: Option[String] = myMap.get("key2") //为None
```

# 18. Iterator

```js
//1. 使用
object Test {
   def main(args: Array[String]) {
      val it = Iterator("Baidu", "Google", "Runoob", "Taobao")
      while (it.hasNext){
         println(it.next())
      }
   }
}

//2. 常用函数
it.min
it.max
it.size
it.length
```

# 19. 类和对象

```js
//1. 类声明
class MyClass(initNum1: Int) {
   var age : Int = initNum1
}

//2. 对象声明
object Test {
   def main(args: Array[String]) {
      val me = new MyClass(18);
   }
}

//3. 继承
class MySubClass(override val initNum1: Int,val initNum2 :Int) extends MyClasss(initNum1){
   var ageSum: Int = initNum1 + initNum2
}
```

# 20. 单例对象

```js
// 私有构造方法
class Marker private(val color:String) {
  println("创建" + this)
  override def toString(): String = "颜色标记："+ color
}

// 伴生对象，与类共享名字，可以访问类的私有属性和方法
object Marker{

    private val markers: Map[String, Marker] = Map(
      "red" -> new Marker("red"),
      "blue" -> new Marker("blue"),
      "green" -> new Marker("green")
    )

    def apply(color:String) = {
      if(markers.contains(color)) markers(color) else null
    }


    def getMarker(color:String) = {
      if(markers.contains(color)) markers(color) else null
    }
    def main(args: Array[String]) {
        println(Marker("red"))  
        // 单例函数调用，省略了.(点)符号  
        println(Marker getMarker "blue")  
    }
}
```

# 21. Traits接口
```js
trait Equal {
  def isEqual(x: Any): Boolean
  def isNotEqual(x: Any): Boolean = !isEqual(x)
}

class Point(xc: Int, yc: Int) extends Equal {
  var x: Int = xc
  var y: Int = yc
  def isEqual(obj: Any) =
    obj.isInstanceOf[Point] &&
    obj.asInstanceOf[Point].x == x
}
```

# 22. match case

```js
object Test {
   def main(args: Array[String]) {
      println(matchTest(3))

   }
   def matchTest(x: Int): String = x match {
      case 1 => "one"
      case 2 => "two"
      case _ => "many"
   }
}
```

## 23. 样例类(匿名类)

```js
object Test {
   def main(args: Array[String]) {
    val alice = new Person("Alice", 25)
    val bob = new Person("Bob", 32)
    val charlie = new Person("Charlie", 32)

    for (person <- List(alice, bob, charlie)) {
        person match {
            case Person("Alice", 25) => println("Hi Alice!")
            case Person("Bob", 32) => println("Hi Bob!")
            case Person(name, age) =>
               println("Age: " + age + " year, name: " + name + "?")
         }
      }
   }
   // 样例类
   case class Person(name: String, age: Int)
}
```

# 24. 正则

```js
val pattern = "Scala".r
val str = "Scala is Scalable and cool"
println(pattern findFirstIn str)
```

# 25. trycatch

```js
import java.io.FileReader
import java.io.FileNotFoundException
import java.io.IOException

object Test {
   def main(args: Array[String]) {
      try {
         val f = new FileReader("input.txt")
      } catch {
         case ex: FileNotFoundException => {
            println("Missing file exception")
         }
         case ex: IOException => {
            println("IO Exception")
         }
      } finally {
         println("Exiting finally...")
      }
   }
 }
```

# 26. Extractor
```js
object Test {
   def main(args: Array[String]) {

      println ("Apply 方法 : " + apply("Zara", "gmail.com"));
      println ("Unapply 方法 : " + unapply("Zara@gmail.com"));
      println ("Unapply 方法 : " + unapply("Zara Ali"));

   }
   // 注入方法 (可选)
   def apply(user: String, domain: String) = {
      user +"@"+ domain
   }

   // 提取方法（必选）
   def unapply(str: String): Option[(String, String)] = {
      val parts = str split "@"
      if (parts.length == 2){
         Some(parts(0), parts(1))
      }else{
         None
      }
   }
}
```


# 注:

```js
1. 都与java一样 >>
    运算符,比较符,逻辑符,ifElse,while,doWhile  

2. 判断对象 >>
    isInstanceOf[MyClass]和asInstanceOf[MyClass]

3. 写文件 >>
    val writer = new PrintWriter(new File("test.txt" ))
    writer.write("hello world")
    writer.close()

4. 读屏 >>
    val line = Console.readLine

5. 读文件 >>
    Source.fromFile("test.txt" ).foreach{
      print
    }

```
