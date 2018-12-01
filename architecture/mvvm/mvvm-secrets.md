معماری MVVM از Model, View  و ViewModel  تشکیل شده است.
-ویو همان اکتیویتی یا فرگمنت است، کلا هر چیزی که نقش ویو داشته باشد.
-مدل همان مدل mvp  است، قسمتی از برنامه که لاجیک و بیزینس‌مدل در آن قرار دارد. قسمتی که وظیفه آماده کردن داده‌ها را برعهده دارد.
-ویومدل نقش واسطه بین مدل و ویو را برعهده دارد.

تفاوت‌های ویو‌مدل با پرزنتر:
-ویومدل جایگزین پرزنتر در این بین می‌شود.
-پرزنتر رفرنسی از ویو در خود نگه می‌دارد، اما ویو‌مدل این کار را انجام نمی‌دهد.
-پرزنتر، ویو را به روش قدیمی و با صدازدن متد‌ها آپدیت می‌کند.
-ویومدل dataStream  ارسال می‌کند.
-پرزنتر و ویو رابطه ۱ به ۱ دارند، که مشکل بزرگی است.
-ویو و ویومدل رابطه ۱ به چند دارند.
-ویو مدل نمی‌داند که ویو درحال گوش کردن به آن است.

در MVVM فقط ویو یک رفرنس به ویومدل دارد و خود ویومدل هیچ رفرنسی به ویو نداشته و هیچ ایده‌ای ندارد که این داده‌هایی که از مدل می‌گیرد را چه کسی مصرف می‌کند.



سه روش برای پیاده‌سازی MVVM در اندروید وجود دارد، استفاده از Rxjava, DataBinding, LiveData

در کل بیشتر از یک راه برای پیاده‌سازی این معماری وجود دارد، می‌توانیم از eventBus, RxAndroid, Google's ViewModel with LiveData  و یا کلا از یک Observer Pattern استفاده کنیم.
ویومدل با Observer Pattern و به صورت ری‌اکتیو پیاده می‌شود.


مزیت LiveData نسبت به بقیه روش‌ها این است که 
لایف‌سایکل اویر یا  Lifecycle Aware  است.
یعنی دیگر نیاز نیست تا مشکلات موجود در لایف‌سایکل اکتیویتی را هندل کنیم، بلکه خودش همه کارها را انجام می‌دهد.




نمونه کد
---

https://github.com/hazems/mvvm-sample-app

https://github.com/ankitsharma6466/AndroidKotlinBoilerplate

https://github.com/MindorksOpenSource/android-mvvm-architecture



منابع
---

https://medium.com/@husayn.hakeem/android-by-example-mvvm-data-binding-introduction-part-1-6a7a5f388bf7

https://www.journaldev.com/20292/android-mvvm-design-pattern

https://proandroiddev.com/mvvm-architecture-viewmodel-and-livedata-part-1-604f50cda1

https://android.jlelse.eu/why-to-choose-mvvm-over-mvp-android-architecture-33c0f2de5516
