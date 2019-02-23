Strict Mode
---

<p dir="rtl">
یک ابزار برای برنامه‌نویسان اندروید تا به وسیله آن جاهایی که به صورت اتفاقی روی 
mainThread
از نتورک یا دیسک  و ... استفاده شده را بگوید.
</p>

<p dir="rtl">
برای استفاده از آن در کلاس اپلیکیشن برنامه آن را تنظیم می‌کنیم.
</p>

``` java

 public void onCreate() {
     if (DEVELOPER_MODE) {
         StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder()
                 .detectDiskReads()
                 .detectDiskWrites()
                 .detectNetwork()   // or .detectAll() for all detectable problems
                 .penaltyLog()
                 .build());
         StrictMode.setVmPolicy(new StrictMode.VmPolicy.Builder()
                 .detectLeakedSqlLiteObjects()
                 .detectLeakedClosableObjects()
                 .penaltyLog()
                 .penaltyDeath()
                 .build());
     }
     super.onCreate();
 }

```


source: https://developer.android.com/reference/android/os/StrictMode.html
