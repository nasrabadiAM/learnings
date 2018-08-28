Mock retrofit requests
---

برای ماک کردن ریکوئست‌ها در رتروفیت ۲ از یک interceptor  فیک استفاده می‌کنیم، به این صورت که این اینترسپتور تمام ریکوئست‌ها را گرفته و به جای آنکه به سرور ریکوئست بزند، خودش اطلاعاتی که آن ریکوئست باید برگرداند را از jsonهای آماده در پوشه assets  یا raw  می‌گیرد و به اپ برمی‌گرداند. 
این فایل‌های موجود در asset می‌تواند همنام با end pointمان باشد تا به صورت داینامیک و براساس end point جسون مربوطه را بازگرداند. برای شبیه‌سازی زمانیکه اینترنت نداریم هم می‌توانیم چک کنیم، که آیا اینترنت کاربر وصل است یا خیر و در صورت وصل نبودن اینترنت، به جای ریکوئست فیک، پیام وصل نبودن اینترنت را به او بدهیم.

منابع
---
https://www.youtube.com/watch?v=CcEdjccZgJc

https://questdot.com/android-retrofit-mock-response-tutorial/

https://futurestud.io/tutorials/retrofit-how-to-refresh-an-access-token