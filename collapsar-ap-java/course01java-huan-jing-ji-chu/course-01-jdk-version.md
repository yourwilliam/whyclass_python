# \[course01] JDK 版本

## \[course01] JDK 版本

![](https://ossp.pengjunjie.com/mweb/16279845166249.jpg)

Java6，7，8比较类似，但是Java8到Java11的更新还是比较实用的，建议使用Java11版本。

#### Java SE Support Roadmap

![](https://ossp.pengjunjie.com/mweb/16279872802199.jpg)

从road map来看，JDK 8和JDK 11都是长期版本。 使用的话建议是JDK 8，11，17这些LTS版本。

### Oracle JDK 和 OpenJDK

2018年9月之后，Oracle JDK 正式商用，运行线上业务收费，开发免费。

OpenJDK完全免费，OpenJDK 11 RTS将会由红帽社区进行维护。

所以我们可以在线上使用OpenJDK，开发的时候使用任意版本的JDK。

### JDK 8 特性

#### 1. Lambda表达式&函数式接口

Lambda 表达式，也可称为闭包，它是推动 Java 8 发布的最重要新特性。

Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）。

使用Lambda 表达式可以使代码变的更加简洁紧凑。

**什么是函数式接口？**

Lambda表达式需要函数式接口的支持。

函数式接口是指只有一个抽象方法的接口。

JDK8提供了注解@FunctionInterface在编译时校验函数式接口。

JDK内置的函数式接口在 java.util.function;

例如：Runnable 接口就是一个函数式接口：

![](https://ossp.pengjunjie.com/mweb/16279951366873.jpg)

```java
/**
 * @author yx
 * @since 2021/2/2 15:18
 */
public class JDKRunnable {
    public static void main(String[] args) {
        // 线程 1
        Runnable r1 = new Runnable() {
            @Override
            public void run() {
                System.out.println("JDK8之前的写法");
            }
        };
        // 线程 2
        Runnable r2 = () -> System.out.println("JDK8之后的写法");

        new Thread(r1).start();
        new Thread(r2).start();
    }
}
```

```java
/**
 * 实现 treeSet 的比较器排序
 */
private void comparator() {
    // TreeSet 是一个有序的集合，它的作用是提供有序的Set集合。这是使用比较器排序。
    TreeSet treeSet = new TreeSet<>(new Comparator() {
        @Override
        public int compare(String o1, String o2) {
            return o1.length() - o2.length();
        }
    });
    // Lambda表达式写法
    TreeSet treeSet1 = new TreeSet<>((m, n) -> m.length() - n.length());
    // 方法引用写法
    TreeSet treeSet2 = new TreeSet<>(Comparator.comparingInt(String::length));
}
```

**方法引用介绍**

方法引用通过方法的名字来指向一个方法。

方法引用可以使语言的构造更紧凑简洁，减少冗余代码。

方法引用使用一对冒号 **::**

在我们使用Lambda表达式的时候，`-><span> </span>`右边部分是要执行的代码，即要完成的功能，可以把这部分称作Lambda体。有时候，当我们想要实现一个函数式接口的那个抽象方法，但是已经有类实现了我们想要的功能，这个时候我们就可以用方法引用来直接使用现有类的功能去实现。

**引用方法**

* 对象引用 :: 实例方法名
* 类名 :: 静态方法名
* 类名 :: 实例方法名
* 对象引用 :: 实例方法名

```java
private static void method() {
    Consumer consumer = System.out::println;
    consumer.accept("方法引用 1 之对象引用::实例方法名");
}
```

`System.out`就是一个`PrintStream`类型的对象引用，而`println`则是一个实例方法名，需要注意的是没有括号的哟。其中`Consumer`是**Java内置函数式接口**，下面的例子用到的都是Java内置函数式接口。`Consumer`中的唯一抽象方法`accept`方法参数列表与`println`方法的参数列表相同，都是接收一个`String`类型参数。

1. 类名::静态方法名

```java
    private static void method() {
        Function f = Math::abs;
        final Integer apply = f.apply(-3);
        System.out.println(apply);
    }
```

`Math`是一个类而`abs`为该类的静态方法。`Function`中的唯一抽象方法`apply`方法参数列表与`abs`方法的参数列表相同，都是接收一个`Integer`类型参数。

1. 类名::实例方法名

```java
    private static void method() {
        BiPredicate n = String::equals;
        final boolean test = n.test("aaa", "bbb");
        System.out.println(test);
    }
```

`String`是一个类而`equals`为该类的定义的实例方法。`BiPredicate`中的唯一抽象方法`test`方法参数列表与`equals`方法的参数列表相同，都是接收两个`String`类型参数。

**引用构造器**

```java
private static void method() {
    Function is = StringBuffer::new;
    final StringBuffer sb = is.apply(10);
    System.out.println(sb.capacity());
}
```

`Function`接口的`apply`方法接收一个参数，并且有返回值。在这里接收的参数是`Integer`类型，与`StringBuffer`类的一个构造方法`StringBuffer(int capacity)`对应，而返回值就是`StringBuffer`类型。上面这段代码的功能就是创建一个`Function`实例，并把它`apply`方法实现为创建一个指定初始大小的`StringBuffer`对象。

**引用数组**

```java
private static void method() {
    Functionint[]> fii = int[]::new;
    final int[] apply1 = fii.apply(20);
    System.out.println(apply1.length);

    Function fid = Double[]::new;
    final int[] apply2 = fii.apply(30);
    System.out.println(apply2.length);
}
```

引用数组和引用构造器很像，格式为 **类型\[]::new**，其中类型可以为基本类型也可以是类。

#### 2. Stream流式编程

Stream 流是 java8 中处理数组、集合的抽象概念，他可以指定你希望对集合进行的操作，可以执行非常复杂的查找、过滤和映射数据等操作。

一个Stream表面上与一个集合很类似，但是集合中保存的是数据，而流设置的是**对数据的操作**。

Stream流的特点：

1. Stream 自己不会存储元素
2. Stream 不会改变源对象，相反，他们会返回一个持有结果的新的Stream
3. Stream 操作是延迟执行的，这意味着他们会等到需要结果的时候才去执行
4. Stream 遵循`做什么，而不是怎么做`的原则，只需要描述做什么，而不用考虑程序是怎么实现的

```java
private static void stream() {
        int[] arr = {4, 1, 2, 5, 0, 8, 6, 5};
        // 获取最大值
        final int max = Arrays.stream(arr).max().getAsInt();
        System.out.println(max);
        // 数组中大于3的元素的数量
        final long count = Arrays.stream(arr).filter(e -> e > 3).count();
        System.out.println(count);

        List list = Arrays.asList(
                new Student(1, "花木兰", 25, 66.0),
                new Student(2, "李白", 21, 90.0),
                new Student(3, "诸葛亮", 21, 80.0),
                new Student(4, "公孙离", 18, 100d),
                new Student(5, "不知火舞", 21, 90d),
                new Student(5, "不知火舞", 21, 90d)
        );

        list.stream().filter(e -> e.getScore() >= 90)
                .findFirst()
                .ifPresent(System.out::println);
        Console.log("-----------filter--------------");

        list.stream().skip(1).limit(2).forEach(System.out::println);
        Console.log("------------limit-------------");

        list.stream().skip(3).distinct().forEach(System.out::println);
        Console.log("-------------distinct------------");

        list.stream().mapToInt(Student::getAge).min().ifPresent(System.out::println);
        Console.log("-------------map------------");

        final Set collect = list.stream().map(Student::getName)
            .collect(Collectors.toSet());
        System.out.println(collect);
        Console.log("-------------collect------------");

        final List collect1 = list.stream()
                .sorted(Comparator.comparingDouble(Student::getScore).reversed()
                .thenComparing(Student::getAge)
                .thenComparing(Student::getId))
                .collect(Collectors.toList());
        System.out.println(collect1);
        Console.log("----------sort---------------");

        final boolean b = list.stream().allMatch(e -> e.getAge() 25);
        Assert.isFalse(b);
        // 正则匹配
        final boolean b1 = list.stream()
            .anyMatch(e -> ReUtil.isMatch("^[1-9]\\d*$", e.getId().toString()));
        Assert.isTrue(b1);
        final boolean b2 = list.stream().noneMatch(e -> e.getScore() == 100d);
        Assert.isFalse(b2);
        Console.log("----------------match------------------");
        list.stream().mapToInt(Student::getAge)
                .reduce(Integer::sum)
                .ifPresent(System.out::println);
        Console.log("----------------reduce------------------");

        final DoubleSummaryStatistics collect2 = list.stream()
            .collect(Collectors.summarizingDouble(Student::getScore));
        Console.log(collect2);

    }
```

![](https://ossp.pengjunjie.com/mweb/16279955383254.jpg)

#### 3. 接口默认方法

Java 8 新增了接口的默认方法。

简单说，默认方法就是接口可以有实现方法，而且不需要实现类去实现其方法。

只需在方法名前面加个 default 关键字即可实现默认方法。

**为什么要有这个特性？**

首先，之前的接口是个双刃剑，好处是面向抽象而不是面向具体编程，缺陷是，当需要修改接口时候，需要修改全部实现该接口的类，目前的 java 8 之前的集合框架没有 foreach 方法，通常能想到的解决办法是在JDK里给相关的接口添加新的方法及实现。然而，对于已经发布的版本，是没法在给接口添加新方法的同时不影响已有的实现。所以引进的默认方法。他们的目的是为了解决接口的修改与现有的实现不兼容的问题。

```java
interface Cat {
    /**
     * 接口默认方法
     */
    default void eat() {
        System.out.println("一只小猫爱吃鱼");
    }

    /**
     * Java 8 的另一个特性是接口可以声明（并且可以提供实现）静态方法。
     */
    static void voice() {
        System.out.println("一只小猫喵喵叫");
    }

}

interface Dog {
    default void eat() {
        System.out.println("一只小狗啃骨头");
    }
}

class Animal implements Cat, Dog{

    @Override
    public void eat() {
        // 第一种使用默认实现
        Dog.super.eat();
        // 第二种自己实现
        System.out.println("我是一只新动物");
        // 调用接口的静态方法
        Cat.voice();
    }
}
```

#### 4.日期时间处理

Java 8通过发布新的Date-Time API (JSR 310)来进一步加强对日期与时间的处理。

在旧版的 Java 中，日期时间 API 存在诸多问题，其中有：

* **非线程安全** − java.util.Date 是非线程安全的，所有的日期类都是可变的，这是Java日期类最大的问题之一。
* **设计很差** − Java的日期/时间类的定义并不一致，在java.util和java.sql的包中都有日期类，此外用于格式化和解析的类在java.text包中定义。java.util.Date同时包含日期和时间，而java.sql.Date仅包含日期，将其纳入java.sql包并不合理。另外这两个类都有相同的名字，这本身就是一个非常糟糕的设计。
* **时区处理麻烦** − 日期类并不提供国际化，没有时区支持，因此Java引入了java.util.Calendar和java.util.TimeZone类，但他们同样存在上述所有的问题。

新的日期/时间API的一些设计原则是：

* 不变性：新的日期/时间API中，所有的类都是不可变的，这对多线程有好处。
* 关注点分离：新的API将人可读的日期/时间和机器的日期/时间明确分离，它为日期Date、时间Time、日期时间DateTime、时间戳unix timestamp以及时区定义了不同的类。
* 清晰：在所有的类中，方法都被明确定义 用以完成相同的行为。举个例子，在所有的类中都定义了now()方法、format()方法、parse()方法，而不是像以前那样专门有一个独立的类。为了更好的处理问题，所有的类都使用了工厂模式和策略模式，一旦你使用了其中某个类的方法，与其他类协同工作并不困难。
* 实用操作：所有新的日期 时间 API 类都实现了一系列方法用以完成通用的任务，如：加、减、格式化、解析、从日期时间中提取单独部分，等等。
* 可扩展性：新的日期/时间API是工作在ISO-801日历系统上的，但我们也可以将其应用在非ISO的日历上。

**LocalDate、LocalTime、LocalDateTime**

![](https://ossp.pengjunjie.com/mweb/16279955798114.jpg)

```java
private static void dateTime() {
        LocalDate localDate = LocalDate.now();
        LocalTime localTime = LocalTime.now();
        LocalDateTime localDateTime = LocalDateTime.now();
        Console.log("当前日期是{}, 时间是{}, 日期时间{}", localDate,
                localTime.format(DateTimeFormatter.ofPattern("HH:mm:ss")),
                localDateTime.format(DateTimeFormatter.ofPattern("yyyy-MM-dd                              HH:mm:ss")));
        // 自定义
        LocalDate date = LocalDate.of(2021, Month.AUGUST, 1);
        Console.log("自定义日期{}", date);
        // 设置地区
        LocalDate seoulDate = LocalDate.now(ZoneId.of("Asia/Seoul"));
        LocalTime seoulTime = LocalTime.now(ZoneId.of("Asia/Seoul"));
        LocalDateTime seoul = LocalDateTime.now(ZoneOffset.of("+9"));
        Console.log("首尔日期{}, 首尔时间{}, 首尔日期时间{}", seoulDate,
                seoulTime.format(DateTimeFormatter.ofPattern("HH:mm:ss")),
                seoul.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")));
        // 时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现            在的总秒数。
        Console.log("当前时间转毫秒数{}", localDateTime
                    .toInstant(ZoneOffset.of("+8")).toEpochMilli());

        Console.log("格林威治时间纳秒{}， 北京时间{}", Instant.now(), localDateTime);

        /**
         * 时间差值
         */
        Duration duration = Duration.between(localDateTime, seoul);
        System.out.println(duration);
        /**
         * 计算日期间隔
         */
        Period period = Period.between(date, seoulDate);
        System.out.println(period);

    }
```

![](https://ossp.pengjunjie.com/mweb/16279956203992.jpg)

#### 5.Optional类

从 Java 8 引入的一个很有趣的特性是 Optional 类。Optional 类主要解决的问题是臭名昭著的空指针异常（NullPointerException）这个异常就不多说了，肯定是每个 Java 程序员都非常了解的异常。Optional 的完整路径是 java.util.Optional，使用它是为了避免代码中的 if (obj != null) { } 这样范式的代码，可以采用链式编程的风格。而且通过 Optional 中提供的 filter 方法可以判断对象是否符合条件，在符合条件的情况下才会返回，map 方法可以在返回对象前修改对象中的属性。

**Optional的用处**

本质上，Optional是一个包含有可选值的包装类，这意味着 Optional 类既可以含有对象也可以为空。我们要知道，Optional 是 Java 实现函数式编程的强劲一步，并且帮助在范式中实现。但是 Optional 的意义显然不止于此。我们知道，任何访问对象方法或属性的调用都可能导致 NullPointerException，在这里，我举个简单的例子来说明一下：

```java
String result = test.getName().getTime().getNum().getAnswer();
```

在上面的这个代码中，如果我们需要确保不触发异常，就得在访问每一个值之前对其进行明确地检查，就是使用if else对test等值进行判断是否为null，这很容易就变得冗长，难以维护。为了简化这个过程，Google公司著名的Guava项目引入了Optional类，Guava通过使用检查空值的方式来防止代码污染，并鼓励程序员写更干净的代码。Optional实际上是个容器：它可以保存类型T的值，或者仅仅保存null。Optional提供很多有用的方法，这样我们就不用显式进行空值检测。

**Optional 的构造函数**

Optional 的三种构造方式：Optional.of(obj)， Optional.ofNullable(obj) 和明确的 Optional.empty()

* Optional.of(obj)：它要求传入的 obj 不能是 null 值的, 否则直接报NullPointerException 异常。
* Optional.ofNullable(obj)：它以一种智能的，宽容的方式来构造一个 Optional 实例。来者不拒，传 null 进到就得到 Optional.empty()，非 null 就调用 Optional.of(obj).
* Optional.empty()：返回一个空的 Optional 对象

**Optional 的常用函数**

* isPresent：如果值存在返回true，否则返回false。
* ifPresent：如果Optional实例有值则为其调用consumer，否则不做处理
* get：如果Optional有值则将其返回，否则抛出NoSuchElementException。因此也不经常用。
* orElse：如果有值则将其返回，否则返回指定的其它值。
* orElseGet：orElseGet与orElse方法类似，区别在于得到的默认值。orElse方法将传入的字符串作为默认值，orElseGet方法可以接受Supplier接口的实现用来生成默认值
* orElseThrow：如果有值则将其返回，否则抛出supplier接口创建的异常。
* filter：如果有值并且满足断言条件返回包含该值的Optional，否则返回空Optional。
* map：如果有值，则对其执行调用mapping函数得到返回值。如果返回值不为null，则创建包含mapping返回值的Optional作为map方法返回值，否则返回空Optional。
* flatMap：如果有值，为其执行mapping函数返回Optional类型返回值，否则返回空Optional。

**Optional 应该怎样用**

在使用 Optional 的时候需要考虑一些事情，以决定什么时候怎样使用它。重要的一点是 Optional 不是 Serializable。因此，它不应该用作类的字段。Optional 类可以将其与流或其它返回 Optional 的方法结合，以构建流畅的API。我们来看一个示例，我们不使用Optional写代码是这样的:

```java
public String getName(User user) {
    if (user == null) {
        return "";
    }
    return user.getName();
}
```

接着我们来改造一下上面的代码，使用Optional来改造，我们先来举一个Optional滥用，没有达到流畅的链式API，反而复杂的例子，如下：

```java
public String getName(User user) {
    Optional u = Optional.ofNullable(user);
    if(!u.isPresent()) {
        return "";
    }
    return u.get().getName();
}
```

这样改写非但不简洁，而且其操作还是和第一段代码一样。无非就是用isPresent方法来替代原先user==null。这样的改写并不是Optional正确的用法，我们再来改写一次。

```java
public String getName(User user) {
    return Optional.ofNullable(user)
        .map(u -> u.getName())
        .orElse("");
}
```

这样才是正确使用Optional的姿势。那么按照这种思路，我们可以安心的进行链式调用，而不是一层层判断了。

#### 6.Base64

在Java8中，Base64编码已经成为Java类库的标准。

Java 8 内置了 Base64 编码的编码器和解码器。

Base64工具类提供了一套静态方法获取下面三种BASE64编解码器：

· 基本：输出被映射到一组字符A-Za-z0-9+/，编码不添加任何行标，输出的解码仅支持A-Za-z0-9+/。

· URL：输出映射到一组字符A-Za-z0-9+\_，输出是URL和文件。

· MIME：输出隐射到MIME友好格式。输出每行不超过76字符，并且使用'\r'并跟随'\n'作为分割。编码输出最后没有行分割。

```java
public static void main(String[] args) {
        //编码，加密getEncoder()
        String str = Base64.getEncoder()
            .encodeToString("java8_Base64?".getBytes(StandardCharsets.UTF_8));
        Console.log("标准加密之后的字符串是 {}", str);
        //解码，解密getDecoder()
        byte[] decode = Base64.getDecoder().decode(str);
        Console.log("标准解码 {}", new String(decode, StandardCharsets.UTF_8));

        //URL编码
        str = Base64.getUrlEncoder()
            .encodeToString("dksiofdo+/d,s;".getBytes(StandardCharsets.UTF_8));
        Console.log("加密后字符串是：{}", str);
        //URL解码
        byte[] decode1 = Base64.getUrlDecoder().decode(str);
        Console.log("URL解码后 {}", new String(decode1, StandardCharsets.UTF_8));

        //Mime编码
        str = Base64.getMimeEncoder()
            .encodeToString("dksiofdo+/d,s;ddd".getBytes(StandardCharsets.UTF_8));
        Console.log("加密后字符串是：{}", str);
        //Mime解码
        byte[] decode2 = Base64.getMimeDecoder().decode(str);
        Console.log("Mime解码后 {}", new String(decode2, StandardCharsets.UTF_8));

        /*
        Base64.Encoder getMimeEncoder(int lineLength, byte[] lineSeparator)：
        返回具有给定lineLength的已修改MIME变体的编码器
        （向下舍入到最接近的4的倍数 - 输出在lineLength
        String s = Base64.getMimeEncoder(6, ".?--".getBytes())
                .encodeToString("jimidssafsaa".getBytes(StandardCharsets.UTF_8));
        Console.log("加密后 {}", s);
        byte[] decode3 = Base64.getMimeDecoder().decode(s);
        Console.log("Mime解码后 {}", new String(decode3, StandardCharsets.UTF_8));

    }
```

### JDK11 新特性

#### 1.类型推断

```java
private static void jdk11() {
    var s = "world";
    var list = new ArrayList();
    list.add(s);
    list.add("java");
    list.add("python");
    list.stream().map(e -> "Hello, " + e)
        .forEach(System.out::println);
}
```

局部变量类型推断就是左边的类型直接使用 **var** 定义，而不用写具体的类型，编译器能根据右边的表达式自动推断类型。

#### 2. 字符串加强

String新增了strip()方法，和trim()相比，strip()可以去掉Unicode空格，例如，中文空格：

```java
// 判断字符串是否为空白
" ".isBlank(); // true
// 去除首尾空格
" Javastack ".strip(); // "Javastack"
// 去除尾部空格
" Javastack ".stripTrailing(); // " Javastack"
// 去除首部空格
" Javastack ".stripLeading(); // "Javastack "
// 复制字符串
"Java".repeat(3);// "JavaJavaJava"
// 行数统计
"A\nB\nC".lines().count(); // 3
```

#### 3. 集合加强

自 Java 9 开始，Jdk 里面为集合（List/ Set/ Map）都添加了 of 和 copyOf 方法，它们两个都用来创建不可变的集合，来看下它们的使用和区别。

```java
var list = List.of("Java", "Python", "C");
var copy = List.copyOf(list);
System.out.println(list == copy); // true
```

```java
var list = new ArrayList();
var copy = List.copyOf(list);
System.out.println(list == copy); // false
```

```java
static  List of(E... elements) {
  switch (elements.length) { // implicit null check of elements
    case 0:
        return ImmutableCollections.emptyList();
    case 1:
        return new ImmutableCollections.List12<>(elements[0]);
    case 2:
        return new ImmutableCollections.List12<>(elements[0], elements[1]);
    default:
        return new ImmutableCollections.ListN<>(elements);
  }
}
static  List copyOf(Collection coll) {
    return ImmutableCollections.listCopy(coll);
}
static  List listCopy(Collection coll) {
    if (coll instanceof AbstractImmutableList && coll.getClass() != SubList.class) {
        return (List)coll;
    } else {
        return (List)List.of(coll.toArray());
    }
}
```

可以看出 copyOf 方法会先判断来源集合是不是 AbstractImmutableList 类型的，如果是，就直接返回，如果不是，则调用 of 创建一个新的集合。

示例2因为用的 new 创建的集合，不属于不可变 AbstractImmutableList 类的子类，所以 copyOf 方法又创建了一个新的实例，所以为false.

注意：**使用of和copyOf创建的集合为不可变集合，不能进行添加、删除、替换、排序等操作**，不然会报 java.lang.UnsupportedOperationException 异常。

上面演示了 List 的 of 和 copyOf 方法，Set 和 Map 接口都有。

#### 4.Stream流处理加强

```java
private static void jdk11() {
    var s = "world";
    var list = List.of(s, "java", "python", "go");
    list.stream().map(e -> "Hello, " + e)
        .forEach(System.out::println);
    /**
         * lambda表达式体为 true 打印，遇到 false则不再继续
         */
    list.stream().takeWhile(e -> !StrUtil.startWith(e, "p"))
        .forEach(System.out::println);

    System.out.println("--------------------------------");
    /**
         * lambda表达式体为true不打印，一直到遇到false开始打印
         */
    list.stream().dropWhile(e -> !StrUtil.startWith(e, "p"))
        .forEach(System.out::println);

}

// 输出
Hello, world
Hello, java
Hello, python
Hello, go
world
java
--------------------------------
python
go
```

#### 5.Http Client支持

Http Client 在 Java 9 中就引入了，在 Java 10 中也进行了部分优化修改，但是一直不够成熟，直到 Java 11 对Http Client 进行了完全的改造，使其标准化。

```java
public static void get() throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://127.0.0.1:8084/hc/getTest"))
                .build();
        // 同步
        HttpResponse response =
                client.send(request, HttpResponse.BodyHandlers.ofString());
        System.out.println("同步" + response.statusCode());
        System.out.println("同步" + response.body());
    }

    public static void get1() throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("http://127.0.0.1:8084/hc/getTest"))
                .build();
        // 异步
        client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
                .thenApply(r -> {
                    System.out.println(r.statusCode());
                    return r;
                }).thenApply(HttpResponse::body)
                .thenAccept(System.out::println)
                .join();
    }

    // 异步调用 POST
    public static void asyncPost() throws Exception {
        HttpClient client = HttpClient.newBuilder()
                // http1.1 or http2.0默认2.0
                .version(HttpClient.Version.HTTP_2)
                // 是否遵从服务器发出的重定向
                .followRedirects(HttpClient.Redirect.NORMAL)
                // 超时时间
                .connectTimeout(Duration.ofSeconds(20))
                // 代理
                // 身份认证
                // 等等
                .build();

        String jsonBody = JSONUtil.toJsonStr("HttpClient.....post");

        HttpRequest request = HttpRequest.newBuilder()
                .uri(new URI("http://127.0.0.1:8084/hc/postTest"))
                .header("Content-Type" , "application/json")
                .POST(HttpRequest.BodyPublishers.ofString(jsonBody))
                .build();
        client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
                .thenApply(r -> {
                    System.out.println(r.statusCode());
                    return r;
                }).thenApply(HttpResponse::body)
                .thenAccept(System.out::println)
                .join();
    }
```

#### 6.JShell工具

Java Shell工具是JDK1.9出现的工具， Java Shell工具（JShell）是一个用于学习Java编程语言和Java代码原型的交互式工具。JShell是一个Read-Evaluate-Print循环（REPL），它在输入时评估声明，语句和表达式，并立即显示结果。该工具从命令行运行。

**为什么要使用JShell ？**

使用JShell，您可以一次输入一个程序元素，立即查看结果，并根据需要进行调整。 Java程序开发通常涉及以下过程：

* 写一个完整的程序。
* 编译它并修复任何错误。
* 运行程序。
* 弄清楚它有什么问题。
* 编辑它。
* 重复这个过程。

JShell可帮助您在开发程序时尝试代码并轻松探索选项。您可以测试单个语句，尝试不同的方法变体，并在JShell会话中试验不熟悉的API。JShell不替换IDE。在开发程序时，将代码粘贴到JShell中进行试用，然后将JShell中的工作代码粘贴到程序编辑器或IDE中。

![](https://ossp.pengjunjie.com/mweb/16279961742235.jpg)
