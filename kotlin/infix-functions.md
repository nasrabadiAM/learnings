<div dir="rtl">

infix functions
---
این فانکشن‌ها با کلمه 
infix 
تعریف می‌شوند

مثل: 

```kotlin

infix fun Int.shl(x: Int): Int { ... }

// calling the function using the infix notation
1 shl 2

// is the same as
1.shl(2)

```


با تعریف یک 
infix function
می‌توانیم بدون استفاده از دات آن متد را صدا بزنیم.

یک 
infix function 
باید شرایط زیر را داشته باشد:

۱. باید ممبرفانکشن یا اکستنشن فانکشن باشد

۲.فقط یک پارامتر ورودی داشته باشد.

۳.پارامتر ورودی نباید مقدار دیفالت داشته باشد و نباید varargs باشد




اگر متدی از داخل خد کلاس را صدا می‌زنیم باید حتما 
this 
را در ابتدا بگذاریم

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






</div>
