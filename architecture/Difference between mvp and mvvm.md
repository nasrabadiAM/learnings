
Difference between mvp and mvvm
---
تفاوت اصلی این دو پترن در این است که رابطه بین ویو و پرزنتر یک به یک است درصورتی که رابطه بین ویو و ویو‌مدل یک به چند است، یعنی هر ویو می‌تواند چندین ویو‌مدل داشته باشد.
تفاوت دیگر آن است که پرزنتر رفرنسی از ویو را در خود نگه‌می‌دارد تا بتواند اطلاعاتی که از مدل می‌گیرد را با متد‌کال در ویو آپدیت کند، درصورتی که ویومدل رفرنسی به ویو ندارد و فقط ویو است که رفرنس ویو‌مدل را دارد و اطلاعات ویو‌مدل را observe  می‌کند. 
این observe کردن می‌تواند به هر روشی و با استفاده از هر ابزاری پیاده شود، خواه دیتابایندینگ باشد یا لایو‌دیتا، یا rx و یا خود Observer Pattern.





منابع
---

https://martinfowler.com/eaaDev/uiArchs.html

https://academy.realm.io/posts/eric-maxwell-mvc-mvp-and-mvvm-on-android/

http://www.differencebetween.net/technology/difference-between-mvvm-and-mvp/
