Parcelable چه تفاوتی با serializable دارد؟ از هرکدام در چه‌زمانی و چرا استفاده می‌کنیم؟ وقتی یک کلاسی از این مدل ها می‌شود، دقیقا چه اتفاقی برایش می‌افتد؟
---




serializable
---
<p dir="rtl">
یک اینترفیس خالی بدون هیچ متدی است. کلاسی که این اینترفیس را ایمپلمنت می‌کند، از این نوع خواهد شد. اما برای پروسه serialization & deserialization باید سه متد زیر را هم ایمپلمنت کنیم و اگر نه در صورتی که به استفاده از این متد‌ها نیاز پیدا شود و آن‌ها را ایمپلمنت نرکده باشیم، اکسپشن throw خواهد کرد.
البته برای serialize کردن یک کلاس فقط کافی است، اینترفیس serializable را ایمپلمنت کند، مگر آنکه بخواهیم پروسه سریال‌کردن و دیسریال‌کردن را کاستوم کنیم.
</p>


```java
 * private void writeObject(java.io.ObjectOutputStream out)
 *     throws IOException
 * private void readObject(java.io.ObjectInputStream in)
 *     throws IOException, ClassNotFoundException;
 * private void readObjectNoData()
 *     throws ObjectStreamException;
```

<p dir="rtl">
این متدها باید دقیقا با همین signature  ایمپلمنت شوند.
</p>

<p dir="rtl">
در متد writeObject  وضعیت آبجکت و کلاس‌های مربوط به آن نوشته خواهد شد و در متد readObject  این وضعیت نوشته شده بازخوانی می‌شود.
</p>

<p dir="rtl">
به این صورت می‌توان یک آبجکت را سریال و یا دیسریال کرد: 
</p>

```java

 Employee e = null;
      try {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      } catch (IOException i) {
         i.printStackTrace();
         return;
      } catch (ClassNotFoundException c) {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      
```

<p dir="rtl">
لازم به ذکر است که serializable جزئی از پکیج‌های جاواست. و در java.io  قرار دارد.
</p>

parcelable
---

<p dir="rtl">
یک اینترفیس با چند متد خاص است. کلاسی که این اینترفیس را ایمپلمنت می‌کند، از این نوع خواهد شد. از این اینترفیس برای نوشتن و بازیابی اطلاعات از روی دیسک استفاده می‌شود.
این اینترفیس جزئی است پکیج‌های اندروید است و در android.os  قرار دارد. 
</p>

<p dir="rtl">
یک کلاس ساده که از این اینترفیس استفاده می‌کند، به صورت زیر است
</p>

```java

  public class MyParcelable implements Parcelable {
      private int mData;
 
      public int describeContents() {
          return 0;
      }
 
      public void writeToParcel(Parcel out, int flags) {
          out.writeInt(mData);
      }
 
      public static final Parcelable.Creator&lt;MyParcelable&gt; CREATOR
              = new Parcelable.Creator&lt;MyParcelable&gt;() {
          public MyParcelable createFromParcel(Parcel in) {
              return new MyParcelable(in);
          }
 
          public MyParcelable[] newArray(int size) {
              return new MyParcelable[size];
          }
      };
      
      private MyParcelable(Parcel in) {
          mData = in.readInt();
      }
  }
  
```



تفاوت بین serializable جاوا و parcelable اندروید:
---
<p dir="rtl">
هر دو این‌ها مکانیزم‌های برای نوشتن و بازیابی اطلاعات هستند. که البته فرق‌هایی با هم دارند.
</p>

<p dir="rtl">
اولین تفاوتشان آن است که serializable متعلق به پکیج io جاوا است ولی parcelable متعلق به پکیج os اندروید.
</p>

<p dir="rtl">
فرق بعدی در سرعت و پرفورمنس این دو است، serializable  جاوا از رفلکشن استفاده می‌کند، برای همین سرعت بسیار پایین‌تری نسبت به parcelable  دارد. همچنین serializable جاوا تعداد زیادی آبجکت‌های موقتی تولید می‌کند که کمی برروی garbage collectionجاوا تاثیرگذار است و کار آن را بیشتر میکند. اما parcelable  بسیار سریعتر است و یکی از دلایل اصلی آن به استفاده نکردن از رفلکشن برمی‌گردد. و البته این‌که این ویژگی به شدت برای این هدف optimize شده است.
</p>

<p dir="rtl">
تفاوت بعدی در سادگی استفاده از seializable نسبت به parcelable است که نمونه کدهای آن‌ها را در ابتدای همین مقاله دیدیم.
</p>




لینک مقاله‌ای که درباره این موضوع نوشتم:
---
https://virgool.io/@nasrabadiam/serializable-vs-parcelable-lqmmpsfyfrmp



منابع
---

https://android.jlelse.eu/parcelable-vs-serializable-6a2556d51538

https://stackoverflow.com/questions/3323074/android-difference-between-parcelable-and-serializable

