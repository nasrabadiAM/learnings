نیازمندی‌های کلیدی برای طراحی API
 
---
از استانداردهای وب هر جا که به کار می‌آید استفاده کنید.
وب‌سرویس‌هایتان دولوپر فرندلی باشد و بتوان با مرورگر آن‌ها را پیمایش کرد.
باید ساده، بصری، پایدار برای استفاده و نه تنها ساده بلکه دلپذیر باشد.
باید کار آمد باشد.

یک API یوزر اینترفیس دولوپرهاست، پس باید درباره ux آن به خوبی فکر کنیم.

از urlها و اکشن‌های rest استفاده کنید
---
اصول کلیدی rest میگوید که APIهایتان را به منابع منطقی تقسیم کنید. این منابع با درخواست های HTTP و با متدهای GET, POST, PUT, PATCH, DELETE کار می‌کند.

این ریسورس‌ها و url های شما باید اسم باشند و نه فعل. در اینجا باید در نظر داشته باشید که نباید پیاده‌سازی‌های داخلی را در API نشر دهید.
مثلاً برخی از این اسم‌ها می‌تواند user, ticket و ... باشد.


زمانی که ریسورس‌هایتان را مشخص کردید، نوبت به آن می‌رسد که مشخص کنید که برای هرکدام نیاز به چه اقداماتی دارید و این اقدامات چطور باید انجام شوند؟

برای این تغییرات http متدهای زیر را دارد:
GET /tickets - Retrieves a list of tickets
GET /tickets/12 - Retrieves a specific ticket
POST /tickets - Creates a new ticket
PUT /tickets/12 - Updates ticket #12
PATCH /tickets/12 - Partially updates ticket #12
DELETE /tickets/12 - Deletes ticket #12


خیلی مهم نیست که برای endpointهایتان از اسم جمع استفاده می‌کنید یا جمع، اما برای سادگی از اسامی جمع استفاده کنید.

چطور رابطه‌ها را هندل کنیم؟
---
اگر یک رابطه با ریسورس دیگری وجود داشته باشد، می‌توان به صورت زیر API را پیاده کرد.

GET /tickets/12/messages - Retrieves list of messages for ticket #12
GET /tickets/12/messages/5 - Retrieves message #5 for ticket #12
POST /tickets/12/messages - Creates a new message in ticket #12
PUT /tickets/12/messages/5 - Updates message #5 for ticket #12
PATCH /tickets/12/messages/5 - Partially updates message #5 for ticket #12
DELETE /tickets/12/messages/5 - Deletes message #5 for ticket #12

به عنوان جایگزین، اگر یک رابطه مستقل از ریسورس وجود داشت، بهتر است یک Id برای آن رابطه مشخص کنیم تا در صورت نیاز از آن Id استفاده کرده و به آن رابطه دسترسی داشته باشیم. اما اگر اغلب اوقات به این رابطه نیاز است بهتر است رابطه را embed کرده و بدون زدن درخواست دوم و در همان درخواست اطلاعات رابطه را بازگردانیم.

اگر درخواست در غالب crud نگنجید، چه کار کنیم؟
یکی از راه‌های پیاده‌سازی این مورد با rest استفاده ترکیبی از اکشن‌ها و متدهای رست است، مثل api کیتهای برای استارکردن یک ریپو:

PUT /gists/:id/star and unstar with DELETE /gists/:id/star.



داکیومت
---
باید داکیومنت‌هایتان را پابلیک و کامل قرار دهید، خوب بودن یک api به اندازه خوب بودن داکیومنت آن است.


ورژن گذاری
---
حتما API هایتان را ورژن گذاری کنید و این ورژن گذاری باید در url باشد تا به راحتی در مرورگر قابل استفاده باشد. 
می‌توانید major version ها را در urlقرار داده و minor versionها را در هدر و بر اساس تایم. 


فیلترکردن، سورت‌کردن و سرچ resultها:
---
برای پیاده‌سازی اینها در API بهتر است از کوئری استفاده کنیم.
GET /tickets?sort=-priority - Retrieves a list of tickets in descending order of priority
GET /tickets?sort=-priority,created_at - Retrieves a list of tickets in descending order of priority. Within a specific priority, older tickets are ordered first


محدود کردن فیلدهایی که باید در API برگردانده شوند
---
گاهی اوقات کاربر نیازی به یک سری فیلدها ندارد، در این حالت بهتر است با کوئری فیلدهایی که می‌خواهد، فقط همان‌ها را دریافت کند. مثل:
GET /tickets?fields=id,subject,customer_name,updated_at&state=open&sort=-updated_at


استفاده از json
--- 
برای API ها حتما از json استفاده کنید.


snake_case vs CamelCase
---
بهتر است از مدلی استفاده‌کنید که کلاینت از آن استفاده می‌کند، مثلا در جاوا از camelCase استفاده می‌شود. برای همین اگر کلاینت شما جاوا است از  camelCase استفاده کنید.
 

به صورت پیشفرض pretty print کنید و مطمئن شوید که gzip پشتیبانی می‌شود
---
با gzip کردن به طور متوسط ۶۰ درصد bandwidth کاهش پیدا می‌کند ‌و با فعال کردن pretty print استفاده از API شما بسیار راحت و دلپذیر می‌شود.



به صورت پیشفرض از envelope استفاده نکنید
---
انولوپ را در شرایطی استفاده کنید که کلاینت نمی‌تواند http کد و ... را بخواند و اگرنه در غیر اینصورت کاری اشتباه است.



استتوس‌کدهای مهم http:
---
1xx (Informational): The request was received, continuing process
2xx (Successful): The request was successfully received, understood, and accepted
3xx (Redirection): Further action needs to be taken in order to complete the request
4xx (Client Error): The request contains bad syntax or cannot be fulfilled
5xx (Server Error): The server failed to fulfill an apparently valid request

لینک چیت‌شیت استاتوس‌کدها: 
https://www.cheatography.com/kstep/cheat-sheets/http-status-codes/pdf/


نکته مهم
---
همیشه سعی کنید، برای هر status code خاص http  یک جیسون مدل ثابت برگردانید. مثلا اگر قرار شد ۲۰۰ برگردانیم باید همیشه جیسون مدل این ریسپانس یک مدل خاص باشد.
اما اگر استتوس‌کد مثلا شد ۵۰۰، جیسون مدل هم تغییر خواهد کرد (نه لزوما) و در جیسون مدل جدید مثلا اطلاعات مربوط به ارور باز می‌گردد.
 


در هر صورت زمانی که در طراحی API به مشکل خوردید، ببینید از نظر استفاده‌کننده API، کار درست چیست. همان کار را پیاده کنید.










منابع
---
https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api

https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9
