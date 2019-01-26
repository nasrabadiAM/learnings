infix functions
---
<p dir="rtl">
این فانکشن‌ها با کلمه 
infix 
تعریف می‌شوند

مثل: 
</p>

```kotlin

infix fun Int.shl(x: Int): Int { ... }

// calling the function using the infix notation
1 shl 2

// is the same as
1.shl(2)

```
<p dir="rtl">
با تعریف یک 
infix function
می‌توانیم بدون استفاده از دات آن متد را صدا بزنیم.
</p>

<p dir="rtl">
یک 
infix function 
باید شرایط زیر را داشته باشد:

۱. باید ممبرفانکشن یا اکستنشن فانکشن باشد

۲.فقط یک پارامتر ورودی داشته باشد.

۳.پارامتر ورودی نباید مقدار دیفالت داشته باشد و نباید varargs باشد
</p>



<p dir="rtl">
اگر متدی از داخل خد کلاس را صدا می‌زنیم باید حتما 
this 
را در ابتدا بگذاریم
</p>

```kotlin

class MyStringCollection {
    infix fun add(s: String) { ... }
    
    fun build() {
        this add "abc"   // Correct
        add("abc")       // Correct
        add "abc"        // Incorrect: the receiver must be specified
    }
}

```
