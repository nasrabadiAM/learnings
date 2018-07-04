 adb چیست؟
---

adb و یا Android debug bridge
یک ابزار کامندلاینی است، که با استفاده از آن می‌توانیم خیلی از کارهای اندروید مثل دیباگ برنامه‌ها، نصب برنامه و یا تریس رم را انجام بدهیم.
در واقع دسترسی به Unix shell اندروید را می‌دهد و تمام دستوراتی که می‌توانیم با آن اجرا کنیم.


از چه قسمت‌هایی تشکیل شده
---
این ابزار سه قسمت دارد:
۱- client:
که برروی ماشینی که دیباگ را در آن انجام  می‌دهید، هست و دستورات را ارسال می‌کند.

۲- daemon (adbd):
 که دستورات را در اندروید اجرا می‌کند،  
 adbd 
 در همه دستگاه‌ها به عنوان یک 
Background process
کار می‌کند.

۳- server: 
که ارتباط بین client و deamon را مدیریت می‌کند. 
سرور در ماشینی که توسعه را انجام می‌دهید، به صورت یک background processکار می‌کند.


adb کجاست؟
---
Adb  
در پوشه platform-tools در sdk اندروید وجود دارد.


چطور کار می‌کند
---
زمانی که یک کلاینت adb را اجرا می‌کنیم، ابتدا چک می‌کند که آیا پروسه فعالی برای server وجود دارد یاخیر؟ اگر وجود نداشته باشد، یک پروسه سرور اجرا می‌کند.
زمانی که سرور اجرا می‌شود، به 
Local TCP port 5037 
Bind
می شود و به دستوراتی که از 
adb clientها 
می آید گوش می‌دهد.
تمام 
adb client 
از پورت 5037 برای ارتباط با 
adb server
استفاده می‌کنند.

سپس سرور ارتباطات با هر دستگاه در حال اجرا را برقرار می‌کند.

سرور از بین آی‌پی‌های 5555 تا 5558 پورت‌های فرد را برای emulator ها استفاده می‌کند، که می‌شود 16 تا شبیه‌ساز اول.

هرکجا که سرور یک adb daemon پیدا کند، با آن پورت وصل می‌شود. توجه کنید که هر شبیه‌ساز از یک زوج متوالی از پورت‌ها استفاده می‌کند به این صورت که اعداد زوج برای ارتباط کنسول و اعداد فرد برای ارتباط adb. مثل:
Emulator 1, console: 5554
Emulator 1, adb: 5555
Emulator 2, console: 5556
Emulator 2, adb: 5557
and so on...


به محض آنکه سرور ارتباطات را تنظیم و برقرار کرد، می‌توانیم از دستورات adb استفاده کنیم.

چون ارتباطات و دستورات را server مدیریت می‌کند، می‌توانیم هر دستگاهی را از هر کلاینت یا اسکریپتی مدیریت کنیم.


برای فعال کردن adb debuging در اندروید، از قسمت developer options  این کار را انجام می دهیم.

اتصال با WI-FI
---
ابتدا کامپیوتر و گوشی  را به یک local network یکسان وصل کنید.
گوشی را با کابل به لپتاب وصل کنید.
گوشی را برای گوش دادن به TCP/IP connection  روی پورت 5555  تنظیم کنید:
`adb tcpip 5555`

کابل را جدا کنید.
با IP به گوشی وصل شوید:
`adb connect device_ip_address` 

در نهایت با دستور `adb devices`  مطمئن شوید که ارتباط برقرار شده است.

اگر ارتباط قطع شد: 
۱- ابتدا adb connect را دوباره اجرا کنید.
۲- اگر وصل نشد، با دستور `adb kill-server` 
host را ری‌استارت کنید.
 

کوئری گرفتن دیوایس‌ها
---
با دستور 
`adb devices` و یا `adb devices -l`  می‌توانیم لیست دیوایس‌هایی که به سرور متصل هستند را بگیریم.

وضعیت اتصال هر دستگاه یکی از سه حالت زیر است
--- 
offline: The device is not connected to adb or is not responding.

device: The device is now connected to the adb server. Note that this state does not imply that the Android system is fully booted and operational because the device connects to adb while the system is still booting. However, after boot-up, this is the normal operational state of an device.

no device: There is no device connected.

شبیه‌ساز در لیست نمایش داده نمی‌شود
---
گاهی اوقات ممکن است emulator در حال اجرا باشد ولی در لیست adb وجود نداشته باشد. در شرایطی ممکن است این اتفاق بیفتد. بری جلوگیری از این اتفاق بهتر است ابتدا adb server را اجرا کنیم و بعد شبیه‌ساز را  و همچنین برای اجرای شبیه‌ساز از آپشن -port و یا -ports استفاده نکنید.


ادامه مطالعه
https://developer.android.com/studio/command-line/adb#directingcommands


منابع
---

https://developer.android.com/studio/command-line/adb


