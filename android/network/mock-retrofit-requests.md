Mock retrofit requests
---
<p dir="rtl">
برای ماک کردن ریکوئست‌ها در رتروفیت ۲ از یک interceptor  فیک استفاده می‌کنیم، به این صورت که این اینترسپتور تمام ریکوئست‌ها را گرفته و به جای آنکه به سرور ریکوئست بزند، خودش اطلاعاتی که آن ریکوئست باید برگرداند را از jsonهای آماده در پوشه assets  یا raw  می‌گیرد و به اپ برمی‌گرداند. 
این فایل‌های موجود در asset می‌تواند همنام با end pointمان باشد تا به صورت داینامیک و براساس end point جسون مربوطه را بازگرداند. برای شبیه‌سازی زمانیکه اینترنت نداریم هم می‌توانیم چک کنیم، که آیا اینترنت کاربر وصل است یا خیر و در صورت وصل نبودن اینترنت، به جای ریکوئست فیک، پیام وصل نبودن اینترنت را به او بدهیم.
</p>

<p dir="rtl">
نمونه کد یک Interceptor 
فیک که از پوشه assets
بک‌اند را می‌گیرد:
</p>

```koltin
class FakeMercuryInterceptor(val context: Context) : Interceptor {

    private val fileSuffix = ".json"
    private val contentType = "application/json"

    override fun intercept(chain: Interceptor.Chain?): Response {

        val fileName = getFileName(chain!!)
        val fileContentString = getFileContent(fileName)

        return Response.Builder()
                .code(200)
                .message(fileContentString)
                .request(chain.request())
                .protocol(Protocol.HTTP_1_0)
                .body(ResponseBody.create(MediaType.parse(contentType), fileContentString.toByteArray()))
                .addHeader("content-type", contentType)
                .build()
    }


    private fun getFileName(chain: Interceptor.Chain): String {
        val fileName = chain.request().url().pathSegments()[chain.request().url().pathSegments().size - 1]
        return if (fileName.isEmpty()) "index$fileSuffix" else fileName + fileSuffix
    }

    private fun getFileContent(fileName: String): String {
        val resultInputStream = context.assets.open(fileName)

        val lineList = mutableListOf<String>()

        resultInputStream.bufferedReader().useLines { lines -> lines.forEach { lineList.add(it) } }
        val resultStringBuilder = StringBuilder()
        lineList.forEach { resultStringBuilder.append(it) }
        return resultStringBuilder.toString()
    }
}

```

<p dir="rtl">
و این هم نحوه استفاده از آن:
</p>

```kotlin

        //set best interceptor
        if (BuildConfig.DEBUG) {
            mercuryHttpClient.addInterceptor(FakeMercuryInterceptor(context))
        } else {
            mercuryHttpClient.addInterceptor(MercuryInterceptor())
        }
        
```


منابع
---
https://www.youtube.com/watch?v=CcEdjccZgJc

https://questdot.com/android-retrofit-mock-response-tutorial/

https://futurestud.io/tutorials/retrofit-how-to-refresh-an-access-token
