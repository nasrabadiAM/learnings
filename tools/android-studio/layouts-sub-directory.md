Layouts Sub Directory
===


موضوع
===

ساخت زیرفولدر و فولدربندی resها

آدرس منبع
===

https://medium.com/mindorks/how-to-put-android-layout-files-in-subfolders-1f7cf07ff48f
https://stackoverflow.com/a/22426467/8743629


خلاصه
===

برای آنکه layoutها فولدربندی شوند و این فولدربندی ها را ببینیم باید حتما در project view اندرویداستودیو باشیم.

برای این کار از قسمت نمایش اندروید استودیو وارد project view شوید.

از لایه های خود در فولدر layout بکاپ بگیرید.

دابرکتوری layout  را پاک کنید.

برروی دایرکتوری res  کلیک راست کرده و پوشه ای که می خواهید تمام فایل هایتان در آن باشد را با نام دلخواه بسازید.
من نام این پوشه را layouts می کذارم.

دوباره با همین ترتیب پوشه بندی های کوچکتر خود را بسازید.

حتما این دسته بندی ها را براساس فیچر انجام دهید نه براساس فرگمنت و اکتیویتی و ...

در آخرین مرحله که می خواهید لایه های xml را بگذارید باید حتما یک پوشه با نام layout  بسازید و فایل های مربوط به آن قسمت را در ئوشه layout زیرین بریزید.

بعد از آنکه تمام این کارها را برای همه xml هایتان انجام دادید.

کدهای زیر را به گرادل خود اضافه کنید.

```gradle


android {

 ...
 
    sourceSets {
        main {
            manifest.srcFile 'src/main/AndroidManifest.xml'
            java.srcDirs = ['src/main/java','.apt_generated']
            aidl.srcDirs = ['src/main/aidl','.apt_generated']
            assets.srcDirs = ['src/main/assets']
            res.srcDirs =
                    [
                            '...',
                            'src/main/res/layouts/appdetail',
                            'src/main/res/layouts',
                            'src/main/res'
                    ]
        }
    }
    
```




نتیجه یک خطی
===
این پوشه بندی فقط برای project view مفید است و فقط در آن قسمت قابل دیدن است.

اما به هرحال فایل های xml پروژه را تمیزتر و بهتر می کند.

 
 
دسته‌بندی(پوشه)
===
ابزارها



تگ
===

#xml 

#project-design

#xml-structure

#project-structure

#res



نوع محتوا
===

متن