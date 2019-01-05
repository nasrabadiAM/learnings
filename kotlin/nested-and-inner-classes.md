Nested And Inner Classes
---

می‌توانیم به روش زیر یک نستد کلاس داشته باشیم:

```kotlin
class Outer {
    private val bar: Int = 1
    class Nested {
        fun foo() = 2
    }
}

val demo = Outer.Nested().foo() // == 2
```


و به روش زیر یک Inner Class  داشته باشیم

```koltin
class Outer {
    private val bar: Int = 1
    inner class Inner {
        fun foo() = bar
    }
}

val demo = Outer().Inner().foo() // == 1
```

اینرکلاس‌ها می‌توانند به member  های کلاس بیرونی دسترسی داشته باشند.

اینرکلاس‌ها یک رفرنس به آبجکتی از کلاس بیرونی خود دارند.




Anonymous Class  
ها با کلمه کلیدی object  ساخته می‌شوند:

```koltin
window.addMouseListener(object: MouseAdapter() {

    override fun mouseClicked(e: MouseEvent) { ... }

    override fun mouseEntered(e: MouseEvent) { ... }
})
```

و اگر آن آبجکت یک نمونه از Functional java Interface
باشد به صورت زیر ساخته می‌شود:

```koltin
val listener = ActionListener { println("clicked") }
```

 functional Java interface (i.e. a Java interface with a single abstract method)
