چطور یک پلاگین برای intelij idea بسازیم؟
---



برای ساخت پلاگین برای intelij idea  و یا هرکدام از ابزارهای شرکت jetbrains  از خود intelij idea  استفاده می‌کنیم.

ساخت یک پروژه جدید را انتخاب کرده و intelij platform plugin را انتخاب می‌کنیم.

پلاگین‌ها از نظر عملکرد به چهار دسته زیر تقسیم می شوند:
1. custom languages
2. Frameworks
3. Tools
4. User interface add-ons 

مثلا یک پلاگین ساده می‌تواند این باشد که وقتی یک متنی را انتخاب می‌کنیم، در منو گزینه سرچ در استک‌اورفلو وجود داشته باشد و با زدن روی آن، آن متن در استک‌اور‌فلو سرچ شود.

برای این کار باید یک اکشن تعریف کنیم. اکشن‌ها هسته اصلی پلاگین‌های intelij idea  هستند.
برای تعریف یک اکشن، کلاسی ساخته و آن را از کلاس AnAction  اکستند می‌کنیم.


مثل کلاس زیر: 

```java
import com.intellij.notification.NotificationDisplayType;
import com.intellij.notification.NotificationGroup;
import com.intellij.notification.NotificationType;
import com.intellij.openapi.actionSystem.AnAction;
import com.intellij.openapi.actionSystem.AnActionEvent;

public class Stackoverflow extends AnAction {
    @Override
    public void actionPerformed(AnActionEvent anActionEvent) {
        NotificationGroup noti = new NotificationGroup("", NotificationDisplayType.BALLOON, true);
        noti.createNotification("Hello Ali",
                "This is a Special Hello To you!",
                "Content",
                NotificationType.INFORMATION)
                .notify(anActionEvent.getProject());
    }
}

```

سپس باید مشخصات اکشن نوشته شده را در فایل plugin.xml اضافه کنیم.

```xml
<idea-plugin>
  <id>com.your.company.unique.plugin.id</id>
  <name>Plugin display name here</name>
  <version>1.0</version>
  <vendor email="support@yourcompany.com" url="http://www.yourcompany.com">YourCompany</vendor>

  <description><![CDATA[
      Enter short description for your plugin here.<br>
      <em>most HTML tags may be used</em>
    ]]></description>

  <change-notes><![CDATA[
      Add change notes here.<br>
      <em>most HTML tags may be used</em>
    ]]>
  </change-notes>

  <!-- please see http://www.jetbrains.org/intellij/sdk/docs/basics/getting_started/build_number_ranges.html for description -->
  <idea-version since-build="173.0"/>

  <!-- please see http://www.jetbrains.org/intellij/sdk/docs/basics/getting_started/plugin_compatibility.html
       on how to target different products -->
  <!-- uncomment to enable plugin in all products
  <depends>com.intellij.modules.lang</depends>
  -->

  <extensions defaultExtensionNs="com.intellij">
    <!-- Add your extensions here -->
  </extensions>

  <actions>
    <!-- Add your actions here -->
    <group id="MyPlugin.TopMenu"
           text="_MyPlugin"
           description="MyPlugin Toolbar Menu">
      <add-to-group group-id="MainMenu" anchor="last"/>
      <action id="MyAction"
              class="Stackoverflow"
              text="_MyAction"
              description="MyAction"/>
    </group>
  </actions>

</idea-plugin>
```
  حالا گزینه اجرای پلاگین را زده و منتظر می مانیم تا IDEجدید همراه با پلاگین ما اجرا شود. بعد از آن می توانیم پلاگین خود را تست کنیم.


این مثالی از ساخت یک پلاگین ساده بود. می‌توانیم پلاگین‌های پیچیده‌تر و حرفته‌ای تر را هم مثل همین بسازیم.



منابع
---

https://www.baeldung.com/intellij-new-custom-plugin

https://proandroiddev.com/write-an-android-studio-plugin-part-1-creating-a-basic-plugin-af956c4f8b50
