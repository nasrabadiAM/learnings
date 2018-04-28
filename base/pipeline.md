##what is pipeline in software


pipeline
در نرم افزار به چه معناست؟


معنی لغوی آن خط لوله است.


pipeline 
در نرم افزار از زنجیره ای از عناصر قابل پردازش تشکیل شده است که خروجی هر عنصر یا قسمت ورودی عنصر بعدی است.


معمولا مقداری داده به عنوان buffering در این pipeline جا به جا می شود که به این قسمت های پایپ لاین filter می گوییم.


در حالت کلی pipeline خطی و یک جهته است اما ممکن است دو جهته باشد.



-------------------

pipeline 
ها یک گروه از کارها هستند که به صورت دسته ای در هر مرحله انجام می شود.


همه کارها در یک مرحله به صورت موازی parallel  
 همه کارها در یک مرحله stage به صورت مواری parallel  اجرا می شوند.
 و زمانی که تمام کارهای یک مرحله stage انجام شد وارد مرحله بعدی می شویم.
 
 
نمونه ای از 
pipeline
می تواند مراحل 
ci باشد.

![](https://docs.gitlab.com/ee/ci/img/pipelines.png)





منابع:

https://en.wikipedia.org/wiki/Pipeline_(software)


https://docs.gitlab.com/ee/ci/pipelines.html
