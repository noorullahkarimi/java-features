<div dir="rtl">

# فیچرهای زبان جاوا 

تمامی محتوا از منابع بسیار معتبر و مختلف جمع آوری شده و گردآورنده هیچ مسئولیتی در قبال این مقاله را نمی پذیرد.
صرفا نویسنده گردآورنده ی این محتوا و فرمت بندی است.

## جدول محتوا

- [فیچرهای زبان جاوا](#فیچرهای-زبان-جاوا)
  - [جدول محتوا](#جدول-محتوا)
  - [مقدمه](#مقدمه)
  - [Lambda Expressions (Java 8)](#Lambda-Expressions)
  - [Stream API (Java 8)](#Stream-API)
  - [Default Methods](#Default-Methods)
  - [Functional Interfaces](#Functional-Interfaces)
  - [Optional](#Optional)
  - [Date and Time API](#Date-and-Time-API)
  - [Parallel Streams](#Parallel-Streams)
  - [CompletableFuture](#CompletableFuture)
  - [Nashorn JavaScript Engine](#Nashorn-JavaScript-Engine)
  - [switch](#switch)
  - [New Instance of](#New-Instance-of)
  - [Var](#Var)
  - [Record](#Record)
  - [Multiline String / Text Blocks](#Multiline-String-/-Text-Blocks)
  - [Sealed Classes](#Sealed-Classes)
  - [of() for collections](#of()-for-collections)
  - [NullPointerException meaningful](#NullPointerException-meaningful)



## مقدمه

دانستن امکانات جاوا برای یک توسعه دهنده ی جاوا بسیار مهم است که باید در این باره بداند بنابراین در این فایل تلاش شده که توضیحاتی بسیار ساده ارایه شود که افراد بتوانند با مقایسه ی کدها به مفهوم تغییرات پی ببرند.

## Lambda Expressions

قبل از جاوا 8، برای پیاده‌سازی روش‌های (متدها) متغیر (به عنوان مثال در رابط‌های کاربری) نیاز به نوشتن کدهای طولانی بود:


قدیمی:

```java
// قبل از Java 8
Button button = new Button();
button.setOnAction(new EventHandler<ActionEvent>() {
    public void handle(ActionEvent event) {
        System.out.println("Button clicked");
    }
});

```
با استفاده از عبارت Lambda، می‌توانیم کدها را کوتاه‌تر نماییم:

جدید:

```java
// در Java 8
button.setOnAction(event -> System.out.println("Button clicked"));

```

[برگشت به بالا](#جدول-محتوا)

## Stream API
قبل از جاوا 8، برای پردازش داده‌ها نیاز به حلقه‌های تکرار بود که کدها را پیچیده می‌کرد:


قدیمی:

```java
// قبل از Java 8
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
for (Integer number : numbers) {
    if (number % 2 == 0) {
        System.out.println(number);
    }
}


```
با Stream API، می‌توانیم این کار را با استفاده از عبارت‌های فیلتر و مپ به صورت خلاصه‌تر انجام دهیم:

جدید:

```java
// در Java 8
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
       .filter(number -> number % 2 == 0)
       .forEach(System.out::println);

```

[برگشت به بالا](#جدول-محتوا)


## Default Methods

قبل از جاوا 8، اضافه کردن یک متد به یک رابط باعث نیاز به تغییر کد‌های همه کلاس‌هایی می‌شدند که از آن رابط پیاده‌سازی می‌شدند:

قدیمی:

```java
// قبل از Java 8
interface MyInterface {
    void method1();
    void method2();
}

class MyClass implements MyInterface {
    public void method1() {
        // implementation
    }
    
    public void method2() {
        // implementation
    }
}


```

اما با Default Methods، می‌توانیم متدهای پیش‌فرض را به رابط‌ها اضافه کنیم بدون اینکه کد کلاس‌های پیاده‌سازی‌کننده را تغییر دهیم:

جدید:

```java
// در Java 8
interface MyInterface {
    void method1();
    void method2();
    
    default void defaultMethod() {
        // implementation
    }
}

class MyClass implements MyInterface {
    public void method1() {
        // implementation
    }
    
    public void method2() {
        // implementation
    }
}

```

[برگشت به بالا](#جدول-محتوا)


## Functional Interfaces

قبل از جاوا 8، برای ایجاد یک رابط تابعی، باید یک رابط خاص جدید ایجاد کنیم، که باعث ایجاد کد زائد می‌شد:


قدیمی:

```java
// قبل از Java 8
interface MyFunctionalInterface {
    void myMethod();
}

// استفاده از یک رابط تابعی جداگانه

```

با اضافه شدن انوتیشن @FunctionalInterface و اجازه تعریف متدهای default و static در رابط‌ها، می‌توانیم به راحتی رابط‌های تابعی را تعریف کنیم:


جدید:

```java
// در Java 8
@FunctionalInterface
interface MyFunctionalInterface {
    void myMethod();
    
    default void defaultMethod() {
        // implementation
    }
    
    static void staticMethod() {
        // implementation
    }
}

```

[برگشت به بالا](#جدول-محتوا)

## Optional

قبل از جاوا 8، برای مقابله با مقادیر خالی نیاز به بررسی‌های بیشتری بود:

قدیمی:

```java
// قبل از Java 8
String name = getName();
if (name != null) {
    System.out.println(name.length());
} else {
    System.out.println("Name is null");
}

```
با Optional، می‌توانیم به صورت خلاصه‌تر با مقادیر خالی مقابله کنیم:


جدید:

```java
// در Java 8
Optional<String> optionalName = Optional.ofNullable(getName());
optionalName.ifPresent(name -> System.out.println(name.length()));

```

[برگشت به بالا](#جدول-محتوا)


## Date and Time API

قبل از جاوا 8، API مربوط به تاریخ و زمان کمی پیچیده بود و این باعث می‌شد که بسیاری از برنامه‌نویسان با مشکل مواجه می‌شدند.

قدیمی:

```java
// قبل از Java 8
Date date = new Date();

```

جدید:

```java
// در Java 8
LocalDate date = LocalDate.now();

```

[برگشت به بالا](#جدول-محتوا)


## Parallel Streams

در نسخه‌های قدیمی‌تر، برای پردازش موازی داده‌ها، ممکن بود از روش‌های سنتی مانند استفاده از حلقه‌های تکرار و نخ‌های جداگانه استفاده کنیم. اما با Parallel Streams، می‌توانیم به صورت ساده‌تر داده‌ها را به صورت موازی پردازش کنیم:


قدیمی:

```java
// قبل از Java 8
for (String item : list) {
    System.out.println(item);
}

```

جدید:

```java
// در Java 8
list.parallelStream().forEach(System.out::println);

```

[برگشت به بالا](#جدول-محتوا)


## CompletableFuture

قبل از Java 8، برای اجرای وظایف همزمان ممکن بود از روش‌های سنتی مانند استفاده از ExecutorService استفاده کنیم. اما با CompletableFuture، می‌توانیم به صورت ساده‌تر و زیباتر وظایف را اجرا کنیم:


قدیمی:

```java
// قبل از Java 8
ExecutorService executor = Executors.newFixedThreadPool(5);
executor.submit(new Runnable() {
    public void run() {
        // کاری را همزمان انجام می‌دهد
    }
});

```

جدید:

```java
// در Java 8
CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
    // کاری را همزمان انجام می‌دهد
});

```

[برگشت به بالا](#جدول-محتوا)

## Nashorn JavaScript Engine

در نسخه‌های قدیمی‌تر، برای اجرای اسکریپت‌های JavaScript نیاز به استفاده از کتابخانه‌های شخص ثالث مانند Rhino بود:


قدیمی:

```java
// قبل از Java 8
Context cx = Context.enter();
try {
    Scriptable scope = cx.initStandardObjects();
    cx.evaluateString(scope, "print('Hello, World!');", "<cmd>", 1, null);
} finally {
    Context.exit();
}


```
در جاوا 8، با اضافه شدن Nashorn JavaScript Engine، می‌توانیم به سادگی اسکریپت‌های JavaScript را درون برنامه‌های جاوا اجرا کنیم:

جدید:

```java
// در Java 8
ScriptEngine engine = new ScriptEngineManager().getEngineByName("nashorn");
engine.eval("print('Hello, World!');");

```

[برگشت به بالا](#جدول-محتوا)


## switch 

تغییر switch (v12)

قدیمی:

```java
int day = 3;
switch(day) {
    case 1:
        System.out.println("Sunday");
        break;
    case 2:
        System.out.println("Monday");
        break;
    case 3:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Invalid day");
}

```

جدید:

```java
int day = 3;
switch(day) {
    case 1 -> System.out.println("Sunday");
    case 2 -> System.out.println("Monday");
    case 3 -> System.out.println("Tuesday");
    default -> System.out.println("Invalid day");
}

```

[برگشت به بالا](#جدول-محتوا)

## New Instance of 

در ورژن قدیمی مجبور به تغییر casting بودیم.(v10)

قدیمی:

```java
Object object = Violin;

if (object instanceof Instrument) {
    // تبدیل object به Instrument اگر object نمونه ای از Instrument باشه
    Instrument instrument = (Instrument) object;
    System.out.println(instrument.getMaster());
}
```
اما با ویژگی New Instance of، می‌توانیم به صورت کوتاه‌تر عمل کنیم:

جدید:

```java
Object object = Violin;
//نیازی به cast کردن نیست. و می توانید instrument رو در همین شرط تعریف کرد.
if (object instanceof Instrument instrument){
    System.out.println(instrument.getMaster());
}
```

[برگشت به بالا](#جدول-محتوا)

## Var 

در نسخه‌های قدیمی‌تر، برای تعریف متغیر نیاز به نوشتن نوع داده بود:(v10)

قدیمی:

```java
ArrayList<String> list = new ArrayList<String>();

```
اما با ویژگی Var، می‌توانیم به صورت خودکار نوع داده را تشخیص دهیم:


جدید:

```java

var list = new ArrayList<String>();


```

[برگشت به بالا](#جدول-محتوا)

## Record 

قبل از این ویژگی، برای ساخت یک کلاس ساده باید کد زیادی بنوشتیم:(v14)

قدیمی:

```java
class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // getters and setters
}

```
اما با ویژگی Record، می‌توانیم به صورت کوتاه‌تر کلاس‌های کمینه‌سازی شده‌ای را ایجاد کنیم:

جدید:

```java
record Person(String name, int age) {
    // به صورت خودکار متدهای equals و hashCode و toString تولید می‌شوند
}

```

[برگشت به بالا](#جدول-محتوا)


## Multiline String / Text Blocks 

درنسخه های قدیمی کار با رشته ها خیلی راحت نبود. مثلا برای رفتن به خط جدید از کاراکتر (\n)باید استفاده میکردیم.
که اگر نبود به خط جدید نمی رفت.(v15)

قدیمی:

```java
String html = "<html>\n" +
              "    <body>\n" +
              "        <p>Hello, JavaRush Student</p>\n" +
              "    </body>\n" +
              "</html>\n";
```
اما با ویژگی جدید می توان براحتی بصورت چند خطی نوشت.

جدید:

```java
String html = """
              <html>
                  <body>
                      <p>Hello, JavaRush Student</p>
                  </body>
              </html>
              """;
```

[برگشت به بالا](#جدول-محتوا)


## Sealed Classes 

در نسخه‌های قدیمی‌تر، کنترل بر روی زیرکلاس‌ها به این شکل ممکن بود:(v17)

قدیمی:

```java
// قبل از Java 17
// بدون امکان محدود کردن زیرکلاس‌ها
// و یا تعریف کلاس ها بصورت فاینال برای محدود کردن ارث بری
public final class StringBuffer  extends AbstractStringBuilder {...}

```
اما با ویژگی Sealed Classes، می‌توانیم زیرکلاس‌های یک کلاس را محدود کنیم:

جدید:

```java
// ارث بری فقط برای کلاس های Circle, Rectangle, Triangle

sealed interface Shape permits Circle, Rectangle, Triangle {
    // ...
}


```

[برگشت به بالا](#جدول-محتوا)

## of() for collections 

در نسخه‌های قدیمی‌تر، برای ساخت مجموعه‌ها نیاز به کد طولانی‌تری داشتیم:(v9)

قدیمی:

```java

List<String> colors = new ArrayList<>();
colors.add("Red");
colors.add("Green");
colors.add("Blue");

```
اما با ویژگی of()، می‌توانیم به صورت خلاصه مجموعه‌ها را بسازیم:

جدید:

```java

List<String> colors = List.of("Red", "Green", "Blue");

```

[برگشت به بالا](#جدول-محتوا)


## NullPointerException meaningful 

در نسخه‌های قدیمی‌تر، پیغام خطای NullPointerException خیلی جالب نبود.(v14)

قدیمی:

```java
/String name = null;
System.out.println(name.length()); // خطا NullPointerException بدون اطلاعات بیشتر

```
اما با ویژگی NullPointerException meaningful، اطلاعات بیشتری در مورد علت خطا نشان داده می‌شود. 
اصطلاحا کاربر پسند تر شده است.

جدید:

```java
String name = null;
System.out.println(name.length()); // خطا: NullPointerException: Cannot invoke "String.length()" because "name" is null

```

[برگشت به بالا](#جدول-محتوا)


</div>