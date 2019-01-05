Sealed Classes
---

این کلاس‌ها مشابه Enumm ها در جاوا هستند.
با این تفاوت که Constant
نیستند و می‌توانند وضعیت داشته باشند.


زمانی که می‌خواهیم یک ریسایکلرویو چند تایپی داشته باشیم از Sealed Class ها استفاده می‌کنیم


```koltin
sealed class Expr
data class Const(val number: Double) : Expr()
data class Sum(val e1: Expr, val e2: Expr) : Expr()
object NotANumber : Expr()
```


و جایی که این کلا کاربرد خودش را نشان می‌دهد زمانی است که از when  استفاده می‌کنیم:


```koltin
fun eval(expr: Expr): Double = when(expr) {
    is Const -> expr.number
    is Sum -> eval(expr.e1) + eval(expr.e2)
    NotANumber -> Double.NaN
    // the `else` clause is not required because we've covered all the cases
}
```



کلاس‌هایی که از sealed class  استفاده می‌کنند باید در همان فایلی تعریف شوند که Sealed Class  تعریف شده است.
