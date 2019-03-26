Mockk Library
---

با استفاده از لایبرری mockk می‌توانیم DOCها یا همان دیپندنسی‌های System Under Test را stub کنیم.

در حالت خیلی ساده می‌توانیم بگوییم وقتی متدی از DOC صدا زده شد، فلان کار را بکن و یا فلان مقدار را برگردان.

```kotlin
every { doc2.value2 } returns "6"
```
اما در حالت پیچیده‌تر می توانیم بگوییم: اگر پارامتر ورودی کمتر از ۵ بود فلان کن و اگر نبود بهمان. که این کار را با استفاده از قابلیت Argument Matching این ابزار انجام می‌دهیم.


```kotlin
every { mock.call(more(5)) } returns 1
every { mock.call(or(less(5), eq(5))) } returns -1
```

رفتاری که می‌خواهیم انجام شود، در ساده‌ترین حالت با return مشخص می‌شود، به این صورت که می‌گوییم، فلان مقدار را return کن. مثل مثال‌های بالا.

با استفاده از returnsMany می‌توانیم در هر بار کال شدن به ترتیب مقادیر مختلفی را بازگردانیم.

```kotlin
every { mock1.call(5) } returnsMany listOf(1, 2, 3)
```

همچنین این کار را با استفاده از andThen هم می‌توانیم انجام دهیم:

```kotlin
every { mock1.call(5) } returns 1 andThen 2 andThen 3
```

اگر بخواهیم اکسپشنی Throw شود:

```kotlin
every { mock1.call(5) } throws RuntimeException("error happened")
```

اگر فقط بخواهیم متدی اجرا شود و کلا مقدار بازگشتی نداشته باشد، از just Runs استفاده می‌کنیم:

```kotlin
every { mock1.callReturningUnit(5) } just Runs
```

با استفاده از answer می‌توانیم یک لامبدا فانکشن کاستوم را اجرا کنیم:

```kotlin
every { mock1.call(5) } answers { arg<Int>(0) + 5 }
```

کار دیگری که این لایبرری برای ما انجام می‌دهد، Behavior verification است.
‌اینBehavior verification چک می‌کند که آیا کامپوننت‌های وابسته با ماک‌آبجکت‌ها صدا زده‌شده‌اند یا نه؟
که در کل چهار نوع وریفیکیشن وجود دارد: unordered, ordered, sequential , all.

مثلا این تکه کد چک می‌کند که آیا این دو متد حداقل یک‌بار صدا زده‌شده‌اند یا خیر.

```kotlin
verify {
mock1.call(5)
mock1.call(6)
}
```
در متد وریفای برخلاف every می‌توانیم هر چندتا متد کال داشته باشیم.

می‌توانیم به متد وریفای پارمتر‌های ورودی atMost که پیشفرض INT.MAX_VALUE است و یا atLeast که پیشفرض 1 است را بدهیم.

```kotlin
verify(atLeast = 5, atMost = 7) {
mock1.call(5)
}
```

یا با استفاده از پارامتر exactly می توانیم مشخص کنیم که دقیقا انتظار داریم چندبار صدا زده شود:

```kotlin
verify(exactly = 5) {
mock1.call(5)
}
```

با استفاده از wasNotCalled می‌توانیم مطمئن شویم که متد موردنظر اصلا کال نشده است:

```kotlin
verify {
mock1 wasNot Called
}
```

بعدی verifyAll است که مشابه verify است با این تفاوت که چک می کند که تمام کال‌های انجام شده، تنها کال‌های آن ماک‌آبجکت‌ها باشند.

دو مورد بعدی verifyOrder و verifySequence هستند.

verifySequence به این صورت عمل می‌کند که علاوه برآنکه ترتیب را چک می‌کند، چک می‌کند که کال‌های انجام شده روی ماک آبجکت‌های مورد نظر، تنها کال‌های آن آبجکت‌ها باشند. اما verifyOrder فقط ترتیب کال‌ها را چک می‌کند و این که بین آن‌ها چه اتفاقی می‌افتد برایش مهم نیست.



اگر به مقدار یک پارامتر در every یا verify احتیاج داشته باشیم می‌توانیم از قابلیت Argument Capturing استفاده کنیم.

```kotlin
every {
mock.divide(capture(slot), any())
} answers {
slot.captured * 11
}
```

نوعی از ماک‌ها وجود دارند، به نام Relaxed mocks ها که درواقع می توانیم مقدار بازگشتی را تعریف نکنیم و در این حالت به جای آنکه اکسپشن بگیریم، نال یا صفر و ... می‌گیریم.

به این صورت تعریف می‌کنیم:

```kotlin
val mock = mockk<Divider>(relaxed = true)

mock.divide(5, 2) // returns 0
```


Spies:
این Spies‌ها این قابلیت را به ما می‌دهند که درحالیکه متد اصلی را اجرا می‌کنیم، برای آن expected Behavoir هم تعریف کنیم.

زمانیکه برروی یک آبجکت یک spy می‌سازیم، آن اسپای دقیقا مثل همان آجکت رفتار می‌کند(آن را در خود کپی می‌کند) و همچنین چک می‌کند که متد اصلی صدا زده‌شده باشد.



علاوه بر صحبت‌هایی که تا اینجا شد، برای @MockK, @SpyK , @RelxedMockK می‌توانیم برای استفاده راحت‌تر از انوتیشن‌ها هم استفاده کنیم.



منبع
---

https://blog.kotlin-academy.com/mocking-is-not-rocket-science-basics-ae55d0aadf2b

https://mockk.io/
