چطور در Heterogenous RecyclerView بسازیم و از چند ویوهولدر استفاده کنیم؟
---
<p dir="rtl">
برای اینکار باید از چند ویوهولدر مختلف استفاده کنیم. به ازای هر نوع آیتمی‌ که داریم، یک ویوهولدر مخصوص به آن می‌سازیم و در onCreateViewHolder  با سوییچ‌کیس آیتم مربوط به آن پوزیشن را می‌سازیم.
</p>

```java 

 @NonNull
    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(@NonNull ViewGroup viewGroup, int viewType) {
        LayoutInflater inflater = LayoutInflater.from(viewGroup.getContext());
        View view = inflater.inflate(viewType, viewGroup, false);
        return ViewHolderCreator.getView(viewType, view);
    }
    
```
<p dir="rtl">
کلاس ViewHolderCreator هم به صورت زیر است:
</p>

```java

public class ViewHolderCreator {

    public static RecyclerView.ViewHolder getView(int viewLayout, View view) {
        switch (viewLayout) {
            case R.layout.image_item:
                return new ImageViewHolder(view);
            case R.layout.product_item:
                return new ProductViewHolder(view);
            case R.layout.progressbar_item:
                return new ProgressViewHolder(view);
            default:
                return new ProgressViewHolder(view);
        }
    }
}
```
<p dir="rtl">
متد getViewType هم به صورت زیر خواهد بود:
</p>

```java
    @Override
    public int getItemViewType(int position) {
        if (items.get(position) instanceof Product)
            return R.layout.product_item;
        if (items.get(position) instanceof String)
            return R.layout.image_item;
        if (items.get(position) instanceof Boolean)
            return R.layout.progressbar_item;
        return -1;
    }

```
<p dir="rtl">
در onbindViewHolder  هم با استفاده از یک اینترفیس که متد bind را دارد،که در آن آیتم را می‌دهیم تا به ویو را بایند کند. این اینترفیس  بایند باید در همه ویو‌هولدر‌های مربوط به هر آیتم ایمپلمنت شود. 
</p>
<p dir="rtl">
متد onBindViewHolder  در ادپتر به صورت زیر است:
</p>

```java
 @Override
    public void onBindViewHolder(@NonNull RecyclerView.ViewHolder viewHolder, int position) {
        if (viewHolder instanceof Binder) {
            ((Binder) viewHolder).bind(items.get(position));
        }
    }
```
<p dir="rtl">
و ویو‌هولدر‌ها هم به صورت زیر پیاده‌سازی می‌شوند:
</p>

```java

//ProductViewHolder

public class ProductViewHolder extends RecyclerView.ViewHolder implements Binder {

    private ImageView image;
    private TextView title;
    private TextView desc;

    public ProductViewHolder(@NonNull View itemView) {
        super(itemView);
        image = itemView.findViewById(R.id.product_image);
        title = itemView.findViewById(R.id.product_title);
        desc = itemView.findViewById(R.id.product_desc);
    }

    @Override
    public void bind(Object item) {
        Product product = (Product) item;
        image.setImageResource(R.drawable.lion);
        title.setText(product.getTitle());
        desc.setText(product.getDesc());
    }

}


//ProgressViewHolder

public class ProgressViewHolder extends RecyclerView.ViewHolder implements Binder {

    private ProgressBar progressBar;

    public ProgressViewHolder(@NonNull View itemView) {
        super(itemView);
        progressBar = itemView.findViewById(R.id.progressbar);
    }

    @Override
    public void bind(Object item) {
        Boolean progressVisibility = (Boolean) item;
        if (progressVisibility) {
            progressBar.setVisibility(View.VISIBLE);
        } else {
            progressBar.setVisibility(View.GONE);
        }
    }

}


//ImageViewHolder

public class ImageViewHolder extends RecyclerView.ViewHolder implements Binder {

    private ImageView imageView;
    private TextView imageUrl;

    public ImageViewHolder(@NonNull View itemView) {
        super(itemView);
        imageView = itemView.findViewById(R.id.image);
        imageUrl = itemView.findViewById(R.id.image_url);
    }

    @Override
    public void bind(Object item) {
        String imageUrlStr = (String) item;
        imageUrl.setText(imageUrlStr);
        imageView.setImageResource(R.drawable.panda);
    }

//Binder Interface

public interface Binder {
    void bind(Object object);
}

```
<p dir="rtl">
راه دیگری که می‌توانیم برای پیاده‌سازی  Heterogenous RecyclerView استفاده کنیم، در لینک زیر وجود دارد. این راه بسیار تمیزتر است، اما یک مشکل اساسی دارد و آن هم این است که اضافه کردن آیتم‌های مختلف بین هم‌دیگر در لیست کار سختی است. اگر بتوانیم این مشکل را حل کنیم، استفاده از این راه بیشتر پیشنهاد می‌شود.
</p>

https://stackoverflow.com/a/29394173/8743629

https://github.com/yqritc/RecyclerView-MultipleViewTypesAdapter



چطور یک لیست‌ویو unlimited  داشته باشیم؟
---
<p dir="rtl">
برای اینکار از یک Heterogenous RecyclerView  استفاده می‌کنیم که یکی از آیتم‌های آن progressbar است. با استفاده از یک onScrollListener چک می‌کنیم که آیا لیست به انتها رسیده یا خیر و اگر رسیده بود این آیتم را به انتهای لیست اضافه می‌کنیم و هر موقع که آیتم‌های بعدی لود شدند، آن را حذف کرده و سپس آیتم‌های اضافه شده را به لیست اضافه می‌کنیم.
</p>



چطور خودمان یک لیست‌ مثل کانتکت‌های گوشی با جدا کردن حروف الفبا بنویسیم؟
---
<p dir="rtl">
به این نوع از لیست Sticky Header List  می‌گویند.
</p>
<p dir="rtl">
دو راه برای این کار وجود دارد، یک استفاده از  ItemDecoration و رسم هدر با Canvas  هست و راه دوم استفاده از Layout Manager  هست.
</p>
<p dir="rtl">
در طراحی یک ui اگر نمی‌توانی خودش را بسازی، فیک‌اش را بساز.
 براساس همین اصل، اگر بخواهیم ویژگی sticky header را به ریسایکلرویو اضافه کنیم، باید کلی کار انجام دهیم و ریسایکلرویو را از اول بسازیم، برای همین بهتر است این فیک این ویژگی را اضافه کنیم.
</p>
<p dir="rtl">
برای اضافه کردن sticky header فیک باید از itemDecoration  استفاده کنیم. کلا از itemDecoration  می‌توانیم برای رسم چیزهای اضافه روی ریسایکلرویو استفاده کنیم. مثلا اگر بخواهیم ه ریسایکلرویو قابلیت گرفتن زوم به‌وسیله تاچ و گرفتن مقدار زوم برای بزرگتر کردن فونت را بخواهیم،‌ باید از itemDecoration  کاستوم استفاده کنیم. (مثل اپ sms ال‌جی کا فونت با زوم اضافه می‌شود)
</p>
<p dir="rtl">
برای اضافه کردن sticky header هم از یک item Decoration کاستوم استفاده می‌کنیم. این item decoration  به این صورت کار می‌کند که زمانی که یک آیتم هدر به بالای لیست می‌رسد، آن آیتم را دوباره روی خودش در بالای لیست رسم می‌کند و دیگر هدر موجود در لیست معلوم نیست، بلکه ویویی که مجددا روی آن رسم شده در حال نمایش است. بعد از آن زمانیکه هدر بعدی می‌آید، با یک اسکرول هدر رسم‌شده قبلی بالای هدر بعدی اسکرول می‌شود، تا هدر جدید به بالای لیست برسد و در آن لحظه دوباره مثل قبل هدر روی لیست رسم می‌شود.
</p>

//دو گیف 
<p dir="rtl">
نمونه کد این کار در لینک زیر قرار دارد:
https://stackoverflow.com/a/44327350/8743629 
</p>
<p dir="rtl">
راه دومی که برای این کار استفاده می‌شود، استفاده از یک LayoutManager  کاستوم است که مثال آن در لینک زیر وجود دارد.
https://github.com/ShamylZakariya/StickyHeaders
</p>

https://github.com/bgogetap/StickyHeaders




ارائه ریسایکلرویو realm
---
<p dir="rtl">
از لیست‌ویو در زمانی استفاده می‌شود که لیست‌هایی با آیتم‌های تکراری و محتوای ثابت داریم. مثل عکس زیر:
</p>

![simple-setting.jpeg](simple-setting.jpeg)
<p dir="rtl">
اما گاهی اوقات هم از آن‌ها برای لیست‌های پیچیده‌تر با آیتم‌های بیشتر استفاده می‌کردیم. در این مواقع برای استفاده بهینه از مموری از ترکیبی از lazy loading  و استفاده مجدد از ویو‌ها قبلی استفاده می‌کردیم.
</p>

**لیست‌ویو یک سری محدودیت و اشتباه داشت:**
<p dir="rtl">
 استفاده نادرست از مموری و مشکلات مربوط به آن
نوشتن کلی کد برای reuseکردن ویو‌ها و استفاده بهینه از ویوها که باید توسط لیست‌ویو انجام می‌شد ولی توسط برنامه ندل می‌شد.
طراحی ناقص API
ویو آیتم کلیک‌لیسنر و آیتم کلیک لیسنر خود لیست‌ویو؟؟؟
انیمیشن‌ها
پیاده‌سازی لایه‌های پیچیده‌تر مثل GridView, Horizontal ListView, Staggerd GridView و... .
</p>

<p dir="rtl">
ریسایکلرویو تمام محدودیت‌ها و اشتباهات لیست‌ویو را برطرف کرده است.
</p>

**ریسایکلرویو از سه قسمت اصلی تشکیل شده است:**

-لیوت منیجر (Layout Manager): کار این قسمت جایگذاری آیتم‌ها در جای مناسب است و مسئولیت پوزیشن آیتم‌ها را بر عهده دارد.

-آیتم انیمیتور (Item Animator):  مسئولیت انیمیشن آیتم‌ها بر عهده این قسمت است.

-ادپتر (Adapter): مسئولیت فراهم‌کردن ویو‌ها نیز به عهده این قسمت می‌باشد.

<p dir="rtl">
 واقع ریسایکلرویو طوری طراحی شده است که به ماژولارترین حالت ممکن باشد، یعنی اگر خواستیم یک ویژگی جدید مثل Drag & Drop  داشته باشیم، نیاز نیست کار جدیدی کنیم، فقط قسمت تاچ جدیدی به ریسایکلر‌ویو می‌دهیم.
 در واقع نیامده‌ای چیز جدیدی برای ریسایکلر بنویسیم، بلکه هر ماژولی خواستیم به آن اضافه می‌کنیم.
</p>

استفاده درست از ریسایکلرویو
---
<p dir="rtl">
ویو‌ها در اندروید به وسیله requestLayout  اعلام می‌کنند که سایزشون تغییر کرده و باید دوباره اندازه‌گیری شوند. با شروع این کار هر ویو از پدر خودش  در درخت ویو‌ها می‌خواهد که اندازه‌اش را دوباره محاسبه و تنظیم کند. این کار همینطور به صورت بازگشتی ادامه پیدا می‌کند تا به ریشه ویو‌ها برسیم و در آنجاست که ریشه فریم بعدی را صدا زده و از فرزندانش می‌خواهد تا همین کار را کنند و همچنین اندازه‌های خودشان را محاسبه و بگویند.
</p>
<p dir="rtl">
این کار در ریسایکلرویو  پرهزینه است، چرا که همه ویو‌ها می‌خواهند از ابتدا رسم شوند. برای همین از SetFixedSize  در آنها استفاده می‌کنیم. مثال این مورد در هنگام لودکردن عکس‌ها می‌باشد. به این صورت که ابتدا تمام آیتم‌ها لود می‌شوند و بعد از آنکه عکسی دانلود شد و خواست لود شود، به پرنت خود می‌گوید که سایز من تغییر کرده و requestLayout می‌کند و این کار تا لایه ریشه ادامه پیدا می‌کند و هر بار که عکسی لود شود این کار تکرار می‌شود. 
</p>
<p dir="rtl">
در مثال بالا برای بالابردن پرفورمنس برای عکس‌ها ک سایز فیکسی تعیین می‌کنیم، با این کار هر بار که عکسی دانلود شود، به جای آنکه requestLayout کنیم و از همه ویو‌ها بخواهیم تا دوباره محاسبه و رسم شوند، فقط از آن‌ها می‌خواهیم که دوباره رسم شوند و این کار پرفورمنس را بسیار بالا می‌برد.
</p>
<p dir="rtl">
کار دیگری که برای بالا بردن پرفورمنس میشه کرد، اینه که قبل از ست کردن ویو چک کنیم که آیا اندازه تصویر تغییر خواهد کرد یا خیر. اگر تغییر می‌کند، requestLAyout را صدا بزنیم و در غیر اینصورت فقط invalidae کنیم.
</p>
<p dir="rtl">
اگر بخواهیم از Staggerd GridView  استفاده کنیم، باید مطمئن شویم که ایمیج‌هایی که در این نوع لیست لود می‌شوند، با نسبت عرض و طول درستی لود خواهند شد. چرا که اگر نسبت درست نباشد و یکی از ایمج‌ها هنوز لود نشده باشد، عکس‌های دیگر به جای آن بزگ می‌شوند و نسبت طول به عرض عکس‌ها به هم خواهد خورد. برای حل این مشکل و یا در onMeasure  ایمج‌ویو و یا ویو‌های این مدلی که aspectRatio یا نسبت طول به عرض مهم است و اگر حفظ نشود، تصویر به هم می‌خورد، می‌توانیم طول را حساب کرده و عرض را بر اساس aspectRatio   محاسبه کنیم.
</p>
<p dir="rtl">
کار دیگری که برای بهینه کردن ریسایکلرویو می‌توانیم انجام دهیم، استفاده از SortedList  است. با استفاده از این نوع لیست  و ایمپلمنت کردن سه متد داخلی آن، می‌توانیم در ریسایکلرویو به پرفورمنس بهتری برسیم. ریسایکلر این طور کار می‌کند که چک می‌کند آیا این آیتم، آیتم جدید است یا خیر و اگر جدید نباشد دیگر کل لیست را از ابتدا رسم نمی‌کند و فقط آیتم‌های جدید را رسم می‌کند.
</p>
<p dir="rtl">
کار دیگری که SortedList  برای ما انجام می‌دهد آن است که دیگر نیازی نیست تا خودمان ادپتر را notify کنیم، بلکه خود SortedList   این کار را انجام خواهد داد.
</p>
<p dir="rtl">
اما ابزار بهتری که برای آپدیت ریسایکلرویو استفاده می‌شود، DiffUtil  است، که در نسخه‌های بعدی ریسایکلرویو اضافه شده است.
</p>


از لیست‌ویو در کجا‌ها و از ریسایکلر‌ویو در چه جاهایی بهتر است استفاده کنیم؟
---
<p dir="rtl">
در جاهاییکه ویو‌های آیتم‌ها پیچیده و پر حجم هستند و یا تعداد خیلی زیادی آیتم داریم، بهتر است از ریسایکلر استفاده کنیم.
</p>

چرخه‌حیات ویو‌هولدر
---
<p dir="rtl">
چرخه ویو‌هولدر به صوت زیر است:
</p>

![adapter-lifecycle01.png](adapter-lifecycle01.png)

![adapter-lifecycle02.png](adapter-lifecycle02.png)

<p dir="rtl">
در onRecycled()  جای خوبی برای آزاد کردن ریسورس‌های سنگین است. اگر عکس و ... دارید، رفرنس به آن را در این متد از بین ببرید تا gc  آن را پاک کند.
</p>
  
<p dir="rtl">
ریسایگلرویو async  است، یعنی کارها را به‌صورت asyncهندل میکند.
</p>
<p dir="rtl">
نکته‌ای که درباره ریسایکلرویو مهم است آن است که برای  اسکرول کردن به پوریشن خاصی باید ابتدا scrollToPosition را صدا بزنیم و بعد از آن ادپتر را به ریسایکلرویو بدهیم، تا به درستی اسکرول شود. 
</p>

<p dir="rtl">
بهتر است ویو‌هولدر‌هایتان را به صورت درست بنویسید، به دو مثال زیر دقت کنید:
</p>

![sad-viewholder.png](sad-viewholder.png)

![happy-viewholder.png](happy-viewholder.png)


<p dir="rtl">
یکی از برتر‌ی‌های ریسایکلرویو نسبت به لیست‌ویو این است که هر چند نوع ویو‌تایپ که بخواهیم می‌توانیم داشته باشیم.
در این حالت بهتر است در متد getItemViewType  به جای آنکه یک عدد برگردانیم، آی‌دی لایه آن نوع را برگردانیم.
</p>

![view-type-01.png](view-type-01.png)


![view-type-02.png](view-type-02.png)


![view-type-03.png](view-type-03.png)


![view-type-04.png](view-type-04.png)

 <p dir="rtl">
دیلیل اینکه ریسایکلرویو، آیتم کلیک‌لیسنر ندارد، آن است که اگر داشته باشد، یا نباید بتوانیم برروی چیز دیگری در آن آیتم‌ها کلیک کنیم و یا اگر می‌توانیم، داریم یک فانکشنالیتی را دو بار پیاده می‌کنیم و این اشتباه است.
</p>




آیتم دکوریشن (Item Decoration)
---
 <p dir="rtl">
با استفاده از این کلاس می‌توانیم شکل‌هایی خاص را روی آیتم‌های ریسایکلرویو رسم کنیم یا به صورت گروهی هایلایت کنیم یا بین آیتم‌ها Divider  بگذاریم و یا  کارهایی از این قبیل را انجام دهیم.
</p>
 <p dir="rtl">
زمانی که برای رسم divider  از خود ویو استفاده می‌کنیم و یک ویو جداگانه برای آن در نظر می‌گیریم، علاوع بر آنکه پرفورمنس کاهش پیدا می‌کند، لگ هم خواهیم داشت و هنگام swip  کردن، دیوایدر همراه با ویو swip  می‌شود که این درست نیست.
پس بهتر است از item Decoration برای divider  استفاده کنید.
</p>



اسکرول‌ویو با قابلیت swipe
---
 <p dir="rtl">
اگر بخواهیم ریسایکلرویو برای آیتم‌هایش قابلیت swipe داشته باشد،‌ می توانیم از ItemTouchHelper استفاده کنیم.
 با استفاده از این helper  می توانیم swipe آیتم‌ها را بفهمیم و در زمان مناسب اگر خواستیم باتنی چیزی رسم کنیم، برای آنکه در هنگام اسکرول باتن‌ها دوباره رسم شوند هم می توانیم از item Decoration  استفاده کنیم.
</p>

 
 چطور می‌توانیم اسکرول‌ویویی با قابلیت tableView  داشته باشیم و بتوانیم به همه طرف اسکرول کنیم؟
 ---
 <p dir="rtl">
 با استفاده از یک Layout Manager  
 کاستوم می‌توانیم این قابلیت را داشته باشیم. برای اطلاعات بیشتر فایل زیر را ببینید:
 </p>
 
 https://github.com/brkckr/TableView/blob/master/app/src/main/java/com/bullseyedevs/tableview/util/FixedGridLayoutManager.java
 
 
 
 



منابع
---

https://academy.realm.io/posts/360andev-yigit-boyar-pro-recyclerview-android-ui-java/
