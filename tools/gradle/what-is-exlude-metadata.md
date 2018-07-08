این قسمت که خیلی در گرادل استفاده می‌شود، چه کاربردی دارد و برای چه نوشته می‌شود؟
---





., [08.07.18 22:04]

packagingOptions {
        exclude '.readme'
        exclude 'LICENSE.txt'
        exclude 'META-INF/DEPENDENCIES'
        exclude 'META-INF/DEPENDENCIES.txt'
        exclude 'META-INF/LGPL2.1'
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/LICENSE.txt'
        exclude 'META-INF/NOTICE'
        exclude 'META-INF/NOTICE.txt'
        exclude 'META-INF/README.txt'
        exclude 'META-INF/dependencies.txt'
        exclude 'META-INF/license.txt'
        exclude 'META-INF/notice.txt'
        exclude 'META-INF/services/javax.annotation.processing.Processor'
        exclude 'META-INF/MANIFEST.MF'
        doNotStrip '*/mips/*.so'
        doNotStrip '*/mips64/*.so'
    }

Javid, [08.07.18 22:32]
[In reply to .]


این META-INF ها همگی متادیتاهایی هستن که معمولا تو کتابخونه‌های جاوایی (jar) وجود دارن، گاهی ممکنه بعضی از این کتابخونه‌ها که تو پروژه استفاده میشن با هم تداخل داشته باشن، برای همین exclude میشن که مشکلی پیش نیاد. نبودشون هم هیچ ضرری برای پروژه نداره.

البته من شخصا مدت‌های خیلی زیادی هست که دیگه لازم نشده برام اینا رو exclude کنم. حدسم اینه که پروژه قدیمیه. می‌تونی حذفشون کنی و تست کنی ببینی برای ساختن apk به مشکلی نمی‌خوری یا نه. از بابت منطق کد خیالت راحت، مشکلی پیش نمیاد.

اون doNotStrip ها هم دارن مشخص می‌کنن که خروجی‌های ndk برای معماری‌های misps و mips64 رو استریپ نکنه (استریپ برای کتاب‌خانه‌های native هست که یه سری چیزی مثل جدول سیمبل‌ها و ... رو حذف میکنه تا حجم فایل نهایی کم بشه)

حالا اینکه چرا اصولا بخوای strip نکنی رو نمی‌دونم، خیلی منطقی به نظر نمیاد، و اینکه اصولا هیچ نرم‌افزار معروفی رو ندیدم که برای ndk بخواد mips رو پشتیبانی کنه چون تقریبا هیچ دیوایسی با معماری mips وجود نداره تو بازار
