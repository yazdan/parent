اینم یه تجربه پراکنده دیگه! همونطور که احتمالا همه میدونید الان بازار
containerها یا همون مجازی سازی سبک در دنیا و خب در ایران داغه. من توی یه
سری پست سعی میکنم ([قسمت اول](http://blog.abyz.ir/1393/08/ligthweight-virtualization-part-1/)) که
راهی رو که خودم برای درک این موضوع طی کردم رو بنویسم. این دفعه در مورد
اینکه آیا این نوع مجازی سازی جدیده یا قدیمی حرف میزنم و اینکه توی هر
سیستم عامل این تکنولوژی چطور پیاده‌سازی شده. کل ایده این هست که سیستم
عامل بتونه یه فضای ایزوله شده رو ایجاد کنه و در اون فضا یه سیستم عامل
دیگه رو به اجرا در بیاره. اولین و قدیمی ترین تکنولوژی که در تمامی سیستم
عامل‌های خانواده یونیکس که لینوکس هم عضوش هست ایجاد شده تکنولوژی
[chroot](http://en.wikipedia.org/wiki/Chroot "Chroot") هست که فضای دیسک
رو از فضای دیسک اصلی ایزوله میکنه. اما بعدی این تکنولوژی‌ها تکمیل شده و
منابع دیگه‌ی سیستم غیر از سیستم فایل هم ایزوله میشن. این ایزوله کردن
اصالتا بر عهده کرنل هر سیستم عامل هست و کرنل هست که مسئولیت این ایزوله
سازی رو برعهده داره پس با توجه به تفاوت‌های سیستم عامل ها تکنولوژی‌های
متفاوتی بوجود اومده که عبارتند از

-   لینوکس
    -   [Linux-VServer](http://en.wikipedia.org/wiki/Linux-VServer "Linux-VServer"):
این تکنولوژی یکی از قدیمی ترین(سال ۲۰۰۱) تکنولوژی‌های مجازی سازی
در سطح سیستم عامل هست که نیاز به تغییر کرنل(پچ شدن کردن) برای
بوجود آوردن امکان ایزوله کردن منابع سیستم هست. این سیستم متن باز
بوده ولی هیچوت تغییراتش به هسته سیستم عامل راه پیدا نکرده
    -   [Parallels Virtuozzo Containers](http://en.wikipedia.org/wiki/Virtuozzo "Virtuozzo"){.mw-redirect} :
این سیستم هم بسیار قدیمی است(سال ۲۰۰۱) و بصورت تجاری توسعه
پیدا کرده.
-   [OpenVZ](http://en.wikipedia.org/wiki/OpenVZ "OpenVZ"): یک محصول
متن بازه که اون هم نیاز به پچ کردن کرنل داره و تغییراتش هیچوت به
درون هسته لینوکس راه پیدا نکرده. شروع توسعه این ابزار به سال
۲۰۰۵ برمیگرده.
    -   ابزارهای مبتنیبر [cgroups](http://en.wikipedia.org/wiki/Cgroups "Cgroups") و [namespaces](http://en.wikipedia.org/wiki/Linux_namespaces "Linux namespaces"){.mw-redirect} در کرنل لینوکس: این تکنولوژی در سال ۲۰۰۶ توسط مهندسان گوگل شروع شده و به کرنل لینوکس راه پیدا کرده. با توجه به این ویژگی‌ها محصولات متفاوتی تولید شده
-   [lmctfy](http://en.wikipedia.org/wiki/Lmctfy "Lmctfy"): این
    ابزار توسط گوگل توسعه پیدا کرده و مورد استفاده قرار
    گرفته. شروع توسعه این ابزار به سال ۲۰۱۳ برمیگرده.
-   [LXC](http://en.wikipedia.org/wiki/LXC "LXC"): این ابزار تا
    اونجایی که من میدونم از دل اوبانتو در اومده و تبدیل به یک
    ابزار قابل استفاده شده. اما به دلیل مستندات محدود خیلی مورد
    استفاده قرار نگرفته. شروع توسعه این ابزار به
    سال ۲۰۰۸ برمیگرده.
-   [Docker](http://en.wikipedia.org/wiki/Docker_%28software%29 "Docker (software)"):
    سازندگان این ابزار ارائه دهنده سرویس
    [paas](http://en.wikipedia.org/wiki/Platform_as_a_service)
    بودند که از روند مشابهی برای
    مدیریت [paas](http://en.wikipedia.org/wiki/Platform_as_a_service)
    خود استفاده می‌کردند و تجربیات خودشون رو در قالب این ابزار
    ارائه دادند. این ابزار به دلیل سادگی، مستندات خوب و معرفی
    راه‌حلهای کارا بسیار مقبولیت پیدا کرده. شروع توسعه این
    ابزار به سال ۲۰۱۳ برمیگرده.
-   [libvir lxc](https://libvirt.org/drvlxc.html): این ابزار هم
    جزئی از کتابخانه
    [libvirt](http://en.wikipedia.org/wiki/Libvirt) برای مدیریت
    تکنولوژی‌های مجازی سازی هست که ابزاری برای مجازی سازی سبک هم
    ارائه کرده.
-   [FreeBSD
    Jail](http://en.wikipedia.org/wiki/FreeBSD_Jail "FreeBSD Jail"){.mw-redirect}:
    در این سیستم عامل از سال ۱۹۹۸ کرنل از ویژگی‌ای به نام
    [jail](http://en.wikipedia.org/wiki/FreeBSD_Jail) پشتیبانی میکنه که
    مجازی سازی سبک رو بوجود میاره. برخلاف لینوکس که چند  ویژگی مجزا کرنل
    برای مجازی سازی سبک استفاده میشه ویژگی
    [jail](http://en.wikipedia.org/wiki/FreeBSD_Jail) در
    [freebsd](http://en.wikipedia.org/wiki/FreeBSD) یک ویژگی یک پارچه
    برای مدیریت مجازی سازی سبک به حساب میاد ابزارهای سطح بالایی هم برای
    این مدیریت این ویژگی بوجود اومده که لیست کوتاه اونها در پایین اومده:
    -   [cbsd](http://www.bsdstore.ru/en/about.html)
    -   [ezjail](http://erdgeist.org/arts/software/ezjail/)
    -   [warden](http://wiki.pcbsd.org/index.php/Warden%C2%AE/9.2)
    -   [iocage](https://github.com/pannon/iocage)
    -   [finch](http://dreamcat4.github.io/finch/)
-   [Solaris
    Containers](http://en.wikipedia.org/wiki/Solaris_Containers "Solaris Containers"):
    این تکنولوژی در هسته سولاریس از سال ۲۰۰۵ وجود داره و من اطلاع زیادی
    از اون ندارم
-   [sysjail](http://en.wikipedia.org/wiki/Sysjail "Sysjail"): این
    تکنولوژی در هسته netbsd و openbsd تا سال ۲۰۰۹ وجود داشته و من اطلاع
    زیادی از اون ندارم
-   [WPARs](http://en.wikipedia.org/wiki/Workload_Partitions "Workload Partitions"):
    یک سیستم خاص منظور برای سیستم
    عامل [AIX](http://en.wikipedia.org/wiki/AIX "AIX"){.mw-redirect} هست(سال ۲۰۰۷)
    و من اطلاع زیادی از اون ندارم
-   [HP-UX Containers (SRP)](http://www.hp.com/go/containers){.external
    .text}: این تکنولوژی
    مختص [HPUX](http://en.wikipedia.org/wiki/HPUX "HPUX"){.mw-redirect} هست(سال ۲۰۰۷)
    که من باز اطلاع خاصی ازش ندارم
-   [Sandboxie](http://en.wikipedia.org/wiki/Sandboxie "Sandboxie"): این
    یه تکنولوژی برای ویندوز هست و من دیدم دوستانی که روی بررسی ویروسها
    کار میکنن ازش استفاده میکنن.

همونطور که میبیند این سیستم و تکنولوژی‌های و ابزارهای مرتبط با اونها
جدید نیستن اما اخیرا دوباره مورد استفاده قرار گرفتن. همین!
