# 1 Lambda标准格式

- 格式由**3个部分**组成：一些参数、一个箭头、一段代码

```
(参数类型 参数名称) -> { 代码语句 }
```

- 小括号内的语法与传统方法参数列表一致：无参数则留空；多个参数则用逗号分隔
- `->`是新引入的语法格式，代表指向动作
- 大括号内的语法与传统方法体要求基本一致
- 

```java
// 无参，无返回值
Runnable r1 = ()->{System.out.println("Hello Lambda!");};
// 有参，有返回值
Comparator<Integer> com = (x,y)->{
    System.out.println("实现函数式接口方法");
    return Integer.compare(x,y);
};
```

# 2 Lambda省略格式

1. 小括号内参数类型可以省略，类型推断

```java
Consumer<String> con = (str)->{System.out.println(str);};
```

2. 如果小括号内**有且仅有一个参**，则小括号可以省略

```java
Consumer<String> con = str->{System.out.println(str);};
```

3. 如果大括号内**有且仅有一个语句**，则无论是否有返回值，都可以省略大括号、return关键字及语句分号

```java
Comparator<Integer> com = (x,y)->Integer.compare(x,y);
```

## 3 Lambda的使用前提

1. 使用Lambda必须具有接口，且要求**接口中有且仅有一个抽象方法**。
   无论是JDK内置的`Runnable`、`Comparator`接口还是自定义的接口，只有当接口中的抽象方法存在且唯一时，才可以使用Lambda
2. 使用Lambda必须具有**上下文推断**。
   也就是方法的参数或局部变量类型必须为Lambda对应的接口类型，才能使用Lambda作为该接口的实例

# 4 函数式接口

## 4.1 定义

- 有且仅有一个抽象方法的接口
- 函数式接口可以适用于Lambda使用的接口
- 可以在一个接口上使用`@FunctionalInterface`注解，这样做可以检查它是否是一个函数式接口。同时javadoc也会包含一条声明，说明这个接口是一个函数式接口
- 在java.util.function包下定义了Java 8 的丰富的函数式接口

## 4.2 自定义函数式接口

- 对于刚刚定义好的MyFunctionalInterface 函数式接口，典型使用场景就是作为方法的参数

```java
public class Demo09FunctionalInterface {    
    // 使用自定义的函数式接口作为方法参数
    private static void doSomething(MyFunctionalInterface inter) {
        inter.myMethod(); // 调用自定义的函数式接口方法
    }
    
    public static void main(String[] args) {
        // 调用使用函数式接口的方法
        doSomething(() ‐> System.out.println("Lambda执行啦！"));
    }
}
```

## 5 函数式编程

## 5.1 Lambda的延迟执行

- 
  有些场景的代码执行后，结果不一定会被使用，从而造成性能浪费。而Lambda表达式是延迟执行的，这正好可以作为解决方案，提升性能

## 5.2 使用Lambda作为参数和返回值

- 如果抛开实现原理不说，Java中的Lambda表达式可以被当作是匿名内部类的替代品
- 如果方法的参数是一个函数式接口类型，那么就可以使用Lambda表达式进行替代
- 使用Lambda表达式作为方法参数，其实就是使用函数式接口作为方法参数

```java
public class Demo04Runnable {
    private static void startThread(Runnable task) {
        new Thread(task).start();
    }
    
	public static void main(String[] args) {
    	startThread(() ‐> System.out.println("线程任务执行！"));
    }
}
```

- 类似地，如果一个方法的返回值类型是一个函数式接口，那么就可以直接返回一个Lambda表达式

# 6 常用函数式接口

|      |      |      |      |
| ---- | ---- | ---- | ---- |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |

函数式接口参数类型返回类型用途
Consumer<T>
消费型接口
T void
对类型为T的对象应用操作，包含方法：
void accept(T t)
Supplier<T>
供给型接口
无T 返回类型为T的对象，包含方法：T get()
Function<T, R>
函数型接口
T R
对类型为T的对象应用操作，并返回结果。结
果是R类型的对象。包含方法：R apply(T t)
Predicate<T>
断定型接口
T boolean
确定类型为T的对象是否满足某约束，并返回
boolean 值。包含方法：boolean test(T t)

## 6.1 Supplier接口

java.util.function.Supplier<T> 接口仅包含一个无参的方法：T get() 。用来获取一个泛型参数指定类型的对
象数据。由于这是一个函数式接口，这也就意味着对应的Lambda表达式需要“对外提供”一个符合泛型类型的对象
数据。

```java
public class Demo04Runnable {
    private static void startThread(Runnable task) {
        new Thread(task).start();
    }
    
	public static void main(String[] args) {
    	startThread(() ‐> System.out.println("线程任务执行！"));
    }
}
```
}
import java.util.Arrays;
import java.util.Comparator;

public class Demo06Comparator {
    private static Comparator<String> newComparator() {
        return (a, b) ‐> b.length() ‐ a.length();
    }

    public static void main(String[] args) {
        String[] array = { "abc", "ab", "abcd" };
        System.out.println(Arrays.toString(array));
        Arrays.sort(array, newComparator());
        System.out.println(Arrays.toString(array));
    }
}

3.2 练习：求数组元素最大值
题目
使用Supplier 接口作为方法参数类型，通过Lambda表达式求出int数组中的最大值。提示：接口的泛型请使用
java.lang.Integer 类。
解答

3.3 Consumer接口
import java.util.function.Supplier;

public class Demo08Supplier {
    private static String getString(Supplier<String> function) {
        return function.get();
    }

    public static void main(String[] args) {
        String msgA = "Hello";
        String msgB = "World";
        System.out.println(getString(() ‐> msgA + msgB));
    }
}
public class Demo02Test {
    //定一个方法,方法的参数传递Supplier,泛型使用Integer
    public static int getMax(Supplier<Integer> sup){
        return sup.get();
    }

    public static void main(String[] args) {
        int arr[] = {2,3,4,52,333,23};
     
        //调用getMax方法,参数传递Lambda
        int maxNum = getMax(()‐>{
           //计算数组的最大值
           int max = arr[0];
           for(int i : arr){
               if(i>max){
                   max = i;
               }
           }
           return max;
        });
        System.out.println(maxNum);
    }
}
java.util.function.Consumer<T> 接口则正好与Supplier接口相反，它不是生产一个数据，而是消费一个数据，
其数据类型由泛型决定。
抽象方法：accept
Consumer 接口中包含抽象方法void accept(T t) ，意为消费一个指定泛型的数据。基本使用如：

当然，更好的写法是使用方法引用。
默认方法：andThen
如果一个方法的参数和返回值全都是Consumer 类型，那么就可以实现效果：消费数据的时候，首先做一个操作，
然后再做一个操作，实现组合。而这个方法就是Consumer 接口中的default方法andThen 。下面是JDK的源代码：

备注：java.util.Objects 的requireNonNull 静态方法将会在参数为null时主动抛出
NullPointerException 异常。这省去了重复编写if语句和抛出空指针异常的麻烦。
要想实现组合，需要两个或多个Lambda表达式即可，而andThen 的语义正是“一步接一步”操作。例如两个步骤组
合的情况：

import java.util.function.Consumer;

public class Demo09Consumer {
    private static void consumeString(Consumer<String> function) {
        function.accept("Hello");
    }

    public static void main(String[] args) {
        consumeString(s ‐> System.out.println(s));
    }
}
default Consumer<T> andThen(Consumer<? super T> after) {
    Objects.requireNonNull(after);
    return (T t) ‐> { accept(t); after.accept(t); };
}
import java.util.function.Consumer;

public class Demo10ConsumerAndThen {
    private static void consumeString(Consumer<String> one, Consumer<String> two) {
        one.andThen(two).accept("Hello");
    }

    public static void main(String[] args) {
        consumeString(
            s ‐> System.out.println(s.toUpperCase()),
            s ‐> System.out.println(s.toLowerCase()));
    }
}
运行结果将会首先打印完全大写的HELLO，然后打印完全小写的hello。当然，通过链式写法可以实现更多步骤的
组合。
3.4 练习：格式化打印信息
题目
下面的字符串数组当中存有多条信息，请按照格式“ 姓名：XX。性别：XX。”的格式将信息打印出来。要求将打印姓
名的动作作为第一个Consumer 接口的Lambda实例，将打印性别的动作作为第二个Consumer 接口的Lambda实
例，将两个Consumer 接口按照顺序“拼接”到一起。

解答

3.5 Predicate接口
有时候我们需要对某种类型的数据进行判断，从而得到一个boolean值结果。这时可以使用
java.util.function.Predicate<T> 接口。
抽象方法：test
Predicate 接口中包含一个抽象方法：boolean test(T t) 。用于条件判断的场景：
public static void main(String[] args) {
    String[] array = { "迪丽热巴,女", "古力娜扎,女", "马尔扎哈,男" };
}
import java.util.function.Consumer;

public class DemoConsumer {
    public static void main(String[] args) {
        String[] array = { "迪丽热巴,女", "古力娜扎,女", "马尔扎哈,男" };
        printInfo(s ‐> System.out.print("姓名：" + s.split(",")[0]),
                  s ‐> System.out.println("。性别：" + s.split(",")[1] + "。"),
                  array);
    }

    private static void printInfo(Consumer<String> one, Consumer<String> two, String[] array) {
        for (String info : array) {
            one.andThen(two).accept(info); // 姓名：迪丽热巴。性别：女。
        }
    }
}

条件判断的标准是传入的Lambda表达式逻辑，只要字符串长度大于5则认为很长。
默认方法：and
既然是条件判断，就会存在与、或、非三种常见的逻辑关系。其中将两个Predicate 条件使用“与”逻辑连接起来实
现“并且”的效果时，可以使用default方法and 。其JDK源码为：

如果要判断一个字符串既要包含大写“H”，又要包含大写“W”，那么：

默认方法：or
与and 的“与”类似，默认方法or 实现逻辑关系中的“或”。JDK源码为：

import java.util.function.Predicate;

public class Demo15PredicateTest {
    private static void method(Predicate<String> predicate) {
        boolean veryLong = predicate.test("HelloWorld");
        System.out.println("字符串很长吗：" + veryLong);
    }

    public static void main(String[] args) {
        method(s ‐> s.length() > 5);
    }
}
default Predicate<T> and(Predicate<? super T> other) {
    Objects.requireNonNull(other);
    return (t) ‐> test(t) && other.test(t);
}
import java.util.function.Predicate;

public class Demo16PredicateAnd {
    private static void method(Predicate<String> one, Predicate<String> two) {
        boolean isValid = one.and(two).test("Helloworld");
        System.out.println("字符串符合要求吗：" + isValid);
    }

    public static void main(String[] args) {
        method(s ‐> s.contains("H"), s ‐> s.contains("W"));
    }
}
default Predicate<T> or(Predicate<? super T> other) {
    Objects.requireNonNull(other);
    return (t) ‐> test(t) || other.test(t);
}
如果希望实现逻辑“字符串包含大写H或者包含大写W”，那么代码只需要将“and”修改为“or”名称即可，其他都不
变：

默认方法：negate
“与”、“或”已经了解了，剩下的“非”（取反）也会简单。默认方法negate 的JDK源代码为：

从实现中很容易看出，它是执行了test方法之后，对结果boolean值进行“!”取反而已。一定要在test 方法调用之前
调用negate 方法，正如and 和or 方法一样：

3.6 练习：集合信息筛选
题目
数组当中有多条“姓名+性别”的信息如下，请通过Predicate 接口的拼装将符合要求的字符串筛选到集合
ArrayList 中，需要同时满足两个条件：
1. 必须为女生；
2. 姓名为4个字。
  import java.util.function.Predicate;

public class Demo16PredicateAnd {
    private static void method(Predicate<String> one, Predicate<String> two) {
        boolean isValid = one.or(two).test("Helloworld");
        System.out.println("字符串符合要求吗：" + isValid);
    }

    public static void main(String[] args) {
        method(s ‐> s.contains("H"), s ‐> s.contains("W"));
    }
}
default Predicate<T> negate() {
    return (t) ‐> !test(t);
}
import java.util.function.Predicate;

public class Demo17PredicateNegate {
    private static void method(Predicate<String> predicate) {
        boolean veryLong = predicate.negate().test("HelloWorld");
        System.out.println("字符串很长吗：" + veryLong);
    }

    public static void main(String[] args) {
        method(s ‐> s.length() < 5);
    }
}

解答

3.7 Function接口
java.util.function.Function<T,R> 接口用来根据一个类型的数据得到另一个类型的数据，前者称为前置条件，
后者称为后置条件。
抽象方法：apply
Function 接口中最主要的抽象方法为：R apply(T t) ，根据类型T的参数获取类型R的结果。
使用的场景例如：将String 类型转换为Integer 类型。
public class DemoPredicate {
    public static void main(String[] args) {
        String[] array = { "迪丽热巴,女", "古力娜扎,女", "马尔扎哈,男", "赵丽颖,女" };
    }
}
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class DemoPredicate {
    public static void main(String[] args) {
        String[] array = { "迪丽热巴,女", "古力娜扎,女", "马尔扎哈,男", "赵丽颖,女" };
        List<String> list = filter(array,
                                   s ‐> "女".equals(s.split(",")[1]),
                                   s ‐> s.split(",")[0].length() == 4);
        System.out.println(list);
    }

    private static List<String> filter(String[] array, Predicate<String> one, 
                                       Predicate<String> two) {
        List<String> list = new ArrayList<>();
        for (String info : array) {
            if (one.and(two).test(info)) {
                list.add(info);
            }
        }
        return list;
    }
}

当然，最好是通过方法引用的写法。
默认方法：andThen
Function 接口中有一个默认的andThen 方法，用来进行组合操作。JDK源代码如：

该方法同样用于“先做什么，再做什么”的场景，和Consumer 中的andThen 差不多：

第一个操作是将字符串解析成为int数字，第二个操作是乘以10。两个操作通过andThen 按照前后顺序组合到了一
起。
请注意，Function的前置条件泛型和后置条件泛型可以相同。
3.8 练习：自定义函数模型拼接
题目
请使用Function 进行函数模型的拼接，按照顺序需要执行的多个函数操作为：
String str = "赵丽颖,20";
import java.util.function.Function;

public class Demo11FunctionApply {
    private static void method(Function<String, Integer> function) {
        int num = function.apply("10");
        System.out.println(num + 20);
    }

    public static void main(String[] args) {
        method(s ‐> Integer.parseInt(s));
    }
}
default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
    Objects.requireNonNull(after);
    return (T t) ‐> after.apply(apply(t));
}
import java.util.function.Function;

public class Demo12FunctionAndThen {
    private static void method(Function<String, Integer> one, Function<Integer, Integer> two) {
        int num = one.andThen(two).apply("10");
        System.out.println(num + 20);
    }

    public static void main(String[] args) {
        method(str‐>Integer.parseInt(str)+10, i ‐> i *= 10);
    }
}
1. 将字符串截取数字年龄部分，得到字符串；
2. 将上一步的字符串转换成为int类型的数字；
3. 将上一步的int数字累加100，得到结果int数字。
  解答
    import java.util.function.Function;

public class DemoFunction {
    public static void main(String[] args) {
        String str = "赵丽颖,20";
        int age = getAgeNum(str, s ‐> s.split(",")[1],
                            s ‐>Integer.parseInt(s),
                            n ‐> n += 100);
        System.out.println(age);
    }

    private static int getAgeNum(String str, Function<String, String> one,
                                 Function<String, Integer> two,
                                 Function<Integer, Integer> three) {
        return one.andThen(two).andThen(three).apply(str);
    }
}

