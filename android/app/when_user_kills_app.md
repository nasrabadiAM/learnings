اگر کاربر اپی را kill کند، چه اتفاقی برای آن اپ می‌افتد؟ چه متدهایی اجرا می‌شوند؟ چه قسمت‌هایی از لایف‌سایکل اکتیویتی اجرا می‌شوند؟
---
<p dir="rtl">
زمانی که کاربر پروسه اپ را از طریق تنظیمات و یا لسیت 
Recent apps 
کیل می‌کند،
پروسه برنامه از ریشه نابود می شود. در اینجا متد 
   onDestroy()
  صدا زده می شود. 
  اما اگر خود اندروید به خاطر کمبود مموری و یا ... پروسه ائ را کیل کند متد 
  onDestroy()
  صدا زده نمی شود.
</p>

<p dir="rtl">
در واقع اپ از نطفه نابود می‌شود.
</p>
