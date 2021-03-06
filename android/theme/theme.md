نحوه استفاده از تم‌ها و مدیریت آن‌ها در اندروید| android theme
---



تم چیست؟ چطور کار می‌کند؟
---
<p dir="rtl">
از lolipop  به بعد نحوه استفاده از تم‌ها تغییر کرد و متریال‌دیزاین به میان آمد. 
</p>

<p dir="rtl">
از آن به بعد تم‌ها در فایل استایل به صورت زیر نوشته می‌شوند:
</p>

```xml
`<resources>
 <!-- inherit from the AppCompat theme -->
 <style name="AppTheme" parent="Theme.AppCompat">
  <!-- your app branding color for the app bar -->
  <item name="colorPrimary">@color/primary</item>
  <!-- darker variant for the status bar and contextual app bars -->
  <item name="colorPrimaryDark">@color/primary_dark</item>
  <!-- theme UI controls like checkboxes and text fields -->
  <item name="colorAccent">@color/accent</item>
 </style>
</resources>
`
```

<p dir="rtl">
اولین رنگی که در تم تعریف می‌شود، colorPrimary یا رنگ اصلی برنامه است. معمولا AppBar  و قسمت‌های اصلی برنامه از این رنگ استفاده می‌کنند.
وقتی از ActionBar  استفاده می‌کنیم، این زنگ به صورت خودکار به پس‌زمینه AppBar نسبت‌داده می‌شود، اما اگر از تولبار استفاده کنیم، باید به صورت زیر خودمان رنگ پس‌زمینه را بدهیم:
</p>

```xml
`<android.support.v7.widget.Toolbar
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:background="?attr/colorPrimary" />`
```

<p dir="rtl">
این نحوه درست رنگ‌دهی به المان‌ها است. زمانیکه به این روش (?attr/) رنگ می‌دهیم، درواقع به اندروید می‌گوییم که رنگ موجود درتم را استفاده کند، به جای آنکه مستقیم رنگ بدهیم.
</p>

<p dir="rtl">
رنگ دوم colorPrimaryDark است، این رنگ ورژن تیره‌تر colorPrimary است که معمولا رنگ 700 از همان دسته رنگ متریال را برای آن انتخاب می‌کنند. 
این رنگ برای status bar تنظیم می‌شود.
</p>

<p dir="rtl">
تنظیمات status bar و تغییر رنگ مربوط به آن در نسخه‌های پایین‌تر از lolipop در دسترس نیست.
</p>

<p dir="rtl">
رنگ سوم colorAccent است. این رنگ در بیشتر قسمت‌های کوچک برنامه دیده می‌شود، مثل سوییچ‌ها و ... .این رنگ بیشتر برای جلب توجه کاربر به قسمت‌های مختف استفاده می‌شود.
</p>

<p dir="rtl">
با استفاده ThemeOverlay  ها، می توانیم به هرتکه ویو‌ یک تم دلخواه بدهیم. می‌توانیم به صورت زیر از ThemeOverlayا استفاده کنیم:
</p>

```xml
`<!-- Ensure text is readable on a dark background by using a 
     Dark ThemeOverlay -->
<android.support.v7.widget.Toolbar
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:background="?attr/colorPrimary"
  android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar" />`
```

<p dir="rtl">
قدرت دیگری که تم‌ها دارند، ساخت تم کاستوم خودمان است که می توانیم به صورت زیر بسازیم:
</p>

```xml
`<style name="ThemeOverlay.AccentSecondary"
       parent="ThemeOverlay.AppCompat">
  <item name=”colorAccent”>@color/accent_secondary</item>
</style>`
```



نمونه کد
---

https://gitlab.com/nasrabadiapps/ziarat-ashura


منابع
---

https://medium.com/google-developers/theming-with-appcompat-1a292b754b35

https://www.hidroh.com/2015/02/16/support-multiple-themes-android-app/

https://android.jlelse.eu/android-developers-we-ve-been-using-themes-all-wrong-eed7755da586

 
