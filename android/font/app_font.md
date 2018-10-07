تعویض و تغییر فونت در برنامه‌های اندرویدی
---

اگر با فونت‌ها در اپ‌های اندرویدی سرو‌کله زده باشید می‌دانید که درست‌کردن آنها کار بسیار سختی است و کلی مشگل وجود دارد.
اما از 
Api level 26
یعنی اندروید ۸
این کار بسیار راحت‌شده و خبر خوب اینکه 
این ویژگی از 
Api level ۱۶
به بالا هم کار می‌کند.


اضافه‌کردن فونت
---
توسط اندروید استودیو و از آدرس
Right-click the res folder and go to New > Android resource directory.
یک پوشه فونت در قسمت
res 
بسازید.

سپس فونت خود را در آن کپی کنید.

حالا می‌توانید، از این فونت مثل بقیه ریسورس‌ها استفاده کنید. 
و آن را به این صورت صدا بزنید.

@font/iransans

به همین سادگی.



برای آنکه از یک فونت برای تمام اپ‌تان استفاده کنید می‌توانید از style ها کمک بگیرید:

فونت خود را توسط آیتم fotFamily به تم برنامه اضافه کنید:

```xml
 <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>

        <item name="android:fontFamily">@font/iransansmobile</item>
    </style>
```

منابع
---

https://developer.android.com/guide/topics/ui/look-and-feel/fonts-in-xml

https://www.youtube.com/watch?v=TfB-TsLFJdM