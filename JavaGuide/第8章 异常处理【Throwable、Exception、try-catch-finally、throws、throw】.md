# 1  异常的体系

- **Throwable父类**
  - **Error**：Java虚拟机无法解决的严重问题。如：JVM系统内部错误、资源耗尽等严重情况。比如：StackOverflowError和OOM。一般不编写针对性的代码进行处理
  - **Exception**
    - **RuntimeException** 运行期异常，需要修正代码
    - **非RuntimeException** 编译期异常，必须处理的，否则程序编译不过

# 2 常见的异常

- java.lang.RuntimeException
  - ClassCastException
  - ArrayIndexOutOfBoundsException
  - NullPointerException
  - ArithmeticException：/0
  - NumberFormatException
  - InputMismatchException
  - 。。。
- java.io.IOExeption
  - FileNotFoundException
  - EOFException
- java.lang.ClassNotFoundException
- java.lang.InterruptedException
- java.io.FileNotFoundException
- java.sql.SQLException

# 3 异常处理机制一：try-catch-finally

## 3.1 异常对象的生成

- 由虚拟机自动生成：程序运行过程中，虚拟机检测到程序发生了问题，如果在当前代码中没有找到相应的处理程序，就会在后台自动创建一个对应异常类的实例对象并抛出——自动抛出
- 由开发人员手动创建：Exception exception = new ClassCastException();——创建好的异常对象不抛出对程序没有任何影响，和创建一个普通对象一样

## 3.2 异常的抛出机制

- 如果一个方法内抛出异常，该异常对象会被抛给调用者方法中处理
- 如果异常没有在调用者方法中处理，它继续被抛给这个调用方法的上层方法，直到异常被处理
- 这一过程称为捕获(catch)异常
- 如果一个异常回到main()方法，并且main()也不处理，则程序运行终止
- 程序员通常只能处理Exception，而对Error无能为力

## 3.3 try-catch-finally语法格式

```java
try{
	...... //可能产生异常的代码
} catch( ExceptionName1 e ){
	...... //当产生ExceptionName1型异常时的处置措施
} catch( ExceptionName2 e ){
	...... //当产生ExceptionName2型异常时的处置措施
}[ finally{
	...... //无论是否发生异常，都无条件执行的语句
} ]
```

- 不论在try代码块中是否发生了异常事件，catch语句是否执行，catch语句是否有异常，catch语句中是否有return，finally块中的语句都会被执行

## 3.4 异常信息-Throwable的相关方法

1. getMessage() ：获取异常信息，返回字符串
2. toString()：获取异常类名和异常信息，返回字符串
3. printStackTrace()：获取异常类名和异常信息，以及异常出现在程序中的位置，返回值void
4. printStackTrace(PrintStream s)：通常用该方法将异常内容保存在日志文件中，以便查阅 

# 4 异常处理机制二：throws

- 在方法声明中用throws语句可以声明抛出异常的列表，throws后面的异常类型可
  以是方法中产生的异常类型，也可以是它的父类

# 5 手动抛出异常：throw

- Java异常类对象除在程序执行过程中出现异常时由系统自动生成并抛出，也可根据需要使用人工创建并抛出

# 6 用户自定义异常类

- 一般地，用户自定义异常类都是RuntimeException的子类
- 自定义异常类通常需要编写几个重载的构造器
- 自定义异常需要提供serialVersionUID
- 自定义的异常通过throw抛出
- 自定义异常最重要的是异常类的名字，当异常出现时，可以根据
  名字判断异常类型

# 7 异常的注意实现

- 子类重写父类方法时，子类的方法必须抛出相同的异常或父类异常的子类
- 父类方法没有异常抛出，子的重写方法不能有异常抛出；如果子类方法内有异常发生，那么子类只能try-catch，不能throws
- 如果父类抛出了多个异常，子类重写父类时，只能抛出相同的异常或者是他的子集，子类不能抛出父类没有的异常

# 8 面试题

## 8.1 编译期异常和运行期异常的区别?

- 编译期异常必须要处理的，否则编译不通过
- 运行期异常可以不处理，也可以处理

## 8.2 finally关键字应用场景

- finally用于释放资源，它的代码永远会执行。特殊情况：在执行到finally之前jvm退出了(比如System.exit(0))

## 8.3 final、finally、finalize的区别?







