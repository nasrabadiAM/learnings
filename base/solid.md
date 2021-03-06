

Solid
---
<p dir="rtl">
در مهندسی نرم‌افزار اصولی وجود دارد به نام 
SOLID 
که پیروی از آن‌ها موجب ساخت نرم‌افزار‌هایی با کیفیت بالاتر می‌شود(از نظر مهندسی نرم‌افزار)
</p>

<p dir="rtl">
کلمه 
SLOID 
مخفف پنج کلمه است.
</p>

1. S - Single Responsibility Prinsiple
2. O - Open/Close Principle
3. L - Liskove Substition Principle
4. I - Interface Segregation Principle
5. D - Dependency Inversion Principle


قانون اول - Single Responsibility Principle
---
<p dir="rtl">
این قانون می‌گوید که هر کلاس باید فقط یک کار را انجام دهد و فقط یک دلیل برای تغییر داشته باشد.
اگر کلاسی بیشتر از یک دلیل برای تغییر دارد، یعنی بیشتر از یک کار را انجام می‌دهد.
</p>
<p dir="rtl">
در کل نباید کلاس‌هایی بنویسیم که 
Smart
باشند و از قسمت‌های مختلف کد و کلاس‌های دیگر خبر داشته باشند. مثلا کلاسی باشد که اگر فلان اتفاق در کلاس دیگری افتاد، کاری را انجام دهد.
</p>
<p dir="rtl">
یکی از مثال‌های نقض این قانون نمونه کد زیر است 
</p>

```java

class Text {
    String text;
    String author;
    int length;

    String getText() { ... }
    void setText(String s) { ... }
    String getAuthor() { ... }
    void setAuthor(String s) { ... }
    int getLength() { ... }
    void setLength(int k) { ... }

    /*methods that change the text*/
    void allLettersToUpperCase() { ... }
    void findSubTextAndDelete(String s) { ... }

    /*method for formatting output*/
    void printText() { ... }
}

```

<p dir="rtl">
 و با تغییرات زیر این قانون در آن رعایت می‌شود:
</p>

```java

class Text {
    String text;
    String author;
    int length;
 
    String getText() { ... }
    void setText(String s) { ... }
    String getAuthor() { ... }
    void setAuthor(String s) { ... }
    int getLength() { ... }
    void setLength(int k) { ... }
 
    /*methods that change the text*/
    void allLettersToUpperCase() { ... }
    void findSubTextAndDelete(String s) { ... }
}
 
class Printer {
    Text text;
 
    Printer(Text t) {
       this.text = t;
    }
 
    void printText() { ... }
}

```

قانون دوم - Open/Close Principle
---
<p dir="rtl">
این قانون می‌گوید که باید بتوانیم از یک کلاس ارث‌بری کنیم بدون آنکه نیاز باشد کلاس پرد را تغییر دهیم.
</p>
<p dir="rtl">
این قانون پایه اصلی 
Maintainability 
و 
Reusability 
در نرم‌افزار است.
</p>
<p dir="rtl">
این قانون جمله 
Open for Extension, Close for Modification
را باین می‌کند، یعنی کلاس‌هایی که می‌نویسیم باید به سختی قابل تغییر باشند، اما به راحتی بتوانیم به آن کدها و فیچر‌های جدید اضافه کرده و آن را توسعه دهیم.
در واقع وقتی کلی وقت می‌گذاریم و کدی با ردون باگ و درست می‌نویسیم، نباید بتوان به راحتی آن را تغییر داد و باعث ایجاد باگ در آن شد، بلکه زمانیکه می‌خواهیم فیچر جدیدی را به برنامه‌امان اضافه کنیم باید برای آن کد‌های جدید هم بنویسیم.
</p>
<p dir="rtl">
برای فهمیدن عمیق‌تر این مورد مثال لینک زیر را نگاه کنید: 
http://joelabrahamsson.com/a-simple-example-of-the-openclosed-principle/
</p>


قانون سوم - Liskove Substition Principle
---
<p dir="rtl">
این قانون می‌گوید که کلاس‌های فرزند نباید به هیچ وجه قرارداد خودشان با پدرشان را بشکنند.
حتی گاهی قوانینی در دنیای واقعی وجود دارند که در دنیای برنامه‌نویسی خیلی منطقی به نظر نمی‌آیند، مثلا همه می دانیم که در ریاضیات هر مربع یک مستطیل است که طول و عرض یکسان دارد.
باتوجه به این موضوع اگر بخواهیم کلاس مستطیل را پیاده‌سازی کنیم دو متد 
setHeight()
و 
setWidth()
را خواهد داشت و اگر کلاس مربع از مستطیل ارث‌بری کند، باید این دو متد را هم در خود پیاده‌سازی کند که می‌دانیم این اشتباه است و اصلا مربع یک مقدار برای طول خود بیشتر ندارد. 
این یک مثال واضح از نقض 
Liskov Substition Principle 
است.
</p>

قانون چهارم - Interface Segregation Principle
---
<p dir="rtl">
کلاینت‌ها نباید اینترفیسی را پیاده کنند که از آن‌ها استفاده نمی‌کنند.
</p>
<p dir="rtl">
مثل 
onTouchListener
در اندروید که همه انترفیس‌های کلیک برروی یک باتن را پیاده کند.
</p>
<p dir="rtl">
برای درست کردن این موضوع به جای آنکه یک اینترفیس چندین متد را در خود داشته باشد، چند اینترفیس جدا داشته باشیم که هرکدام یک متد داشته باشند.
با این کار هرقسمت فقط اینترفیسی را پیاده‌سازی می‌کند که به آن نیاز دارد.
</p>

قانون پنجم - Dependency Inversion Principle
---
<p dir="rtl">
این قانون دو اصل مهم را بیان می‌کند.
</p>
<p dir="rtl">
اصل اول این است که هیچ ماژول یا کلاس 
High Level
ای نباید به کلاس‌های 
Low level 
وابسته باشد، بلکه هر دو اینها باید به ابسترکشن وابسته باشند.
</p>
<p dir="rtl">
اصل دوم هم می‌گوید که ابسترکشن‌ها نباید به جزییات وابسته باشند، بلکه این جزییات هستند که باید به ابسترکشن وابسته باشند.
</p>
<p dir="rtl">
مثلا کلاس پرزنتر نباید به کلاس ویو وابسته باشد، بلکه باید یک اینترفیسی بین این دو قرار بگیرد و پرزنتر با صدا زدن آن اینترفیس که می‌تواند 
Implementation
های مختلفی داشته باشد، کار را انجام دهد و نه با صدا زدن یک متد از کلاس ویو.
</p>


منابع
---

https://www.youtube.com/playlist?list=PLT2xIm2X7W7jh6KggjhwTH9s_8XIlSdOs

https://springframework.guru/principles-of-object-oriented-design/single-responsibility-principle/

http://joelabrahamsson.com/a-simple-example-of-the-openclosed-principle/
</div>


