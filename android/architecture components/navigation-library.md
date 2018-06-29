 کتابخانه نویگیشن اندروید


قوانین نویگیشن
---
-برنامه باید یک شروع مشخص داشته باشد: یعنی برنامه فقط و فقط با یک اکتویتی خاص شروع شود و با همان اکتیویتی به پایان برسد.

-از یک استک برای نمایش وضعیت فعلی نویگیشن یک برنامه استفاده می‌شود:‌ نویگیشن در برنامه باید به صورت Last in First out باشد و همه کار‌ها باید برروی top استک انجام گیرد.

-به وسیله up button  نباید بتوان از اپ خارج شد: یعنی صفحه اول up button نخواهد داشت و همچنین اگر برنامه با deep link باز شود، کاربر باید به وسیله بک یا up button سلسله‌وار به صفحه اول برگشته و بعد برنامه بسته شود.

up button  همان دکمه بالای صفحه در تولبار هست که شبیه بک هست و با زدن آن به صفحه قبلی باز می‌گردیم.

-Up و Back در برنامه‌های ما یکی هستند: up button باید دقیقا مثل back عمل کند.

-رفتن یک کاربر به مقصدی در برنامه باید مثل باز کردن deep linkای به آن مقصد باشد: یعنی بعد از باز شدن deep link با بک زدن یا up button نباید به برنامه دیگری منتقل شویم بلکه باید نویگیشن را تا صفحه اول برنامه خودمان طی کنیم و بعد از برنامه خارج شویم.




پیاده‌سازی نویگیشن به وسیله کتابخانه نویگشین 
---
برای پیاده‌سازی از چیزی به نام navigation graph استفاده می‌کنیم که گراف نویشگیشن در برنامه را نشان می‌دهد.
این گراف شامل destinationهایی است. 

destination به هر صفحه‌ای گفته می‌شود که در برنامه داریم. این مقصد‌ها می‌توانند اکتیویتی، فرگمنت یا کلاسی باشند که ما تعریف می‌کنیم.

 علاوه‌بر destinationها ، چیزی به نام Action داریم که مابین هر دو destination قرار می‌گیرد.
 
  به زبان ساده یک گراف از صفحات برنامه داریم که نود‌های آن صفحات برنامه و روابط بین این نود‌ها Action‌های این گراف هستند.
  
  
  
  
منبع
---
  
  https://developer.android.com/topic/libraries/architecture/navigation/navigation-implementing