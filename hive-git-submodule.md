یکی از ویژگی‌های [git] که به ما امکان ترکیب مخازن مختلف کد را می‌دهد امکان [submodule] است. خیلی وقت‌ها اتفاق می‌افتد که بخشی از پروژه ما در پروژه‌های مختلف مشترک است، و ما در هر پروژه جدیدی که شروع می‌کنیم از آن کد استفاده می‌کنیم. مثلا اگر شما توسعه دهنده قالب برای وردپرس باشید، ممکن است فایلهای جاوا اسکریپت مربوط به اسلایدها صفحه اول در تمام قالب‌هایی که می‌سازید تکرار شوند. ممکن است شما به عنوان یک توسعه دهنده اندروید کلاس‌هایی را برای ارتباط با سرویس‌های اجتماعی توسعه داده باشید که در تمام نرم‌افزارهای شما مورد استفاده قرار گرفته است. ممکن است به عنوان  یک برنامه نویس دسکتاپ، کنترلهایی را برای کارهای خاص تولید کرده باشید که در تمامی پروژه‌ها از آن استفاده می‌کنید. در این حالت با استفاده از [submodule]ها شما می‌توانید کل تاریخچه آن بخش مشترک در پروژه‌هایتان را به عنوان یک مخزن مستقل توسعه داده و از آن در پروژه‌های مختلف استفاده کنید. این کار علاوه تقویت ساختار منطقی پروژه‌هایتان روند رفع ایراد در پروژه‌های مختلف را آسانتر می‌کند.

در واقع [submodule] به شما این امکان را می‌دهد که به درون یک مخزن، یک یا چند مخزن دیگر اضافه کرده و از آنها در کنار هم استفاده کنید. در این نوشته بصورت خلاصه سعی می‌شود که نحوه کار با این ویژگی ارائه شود.

## اضافه کردن یک [submodule]

اضافه کردن یک [submodule] کار راحتی است. کافی است که به خط فرمان رفته و از دستور `git add submodule` استفاده کنید مثال این دستور به شکل زیر است:

```bash
$ git submodule add https://github.com/chaconinc/DbConnector
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
```
بعد از اجرای درست این دستور فایل جدید ‍‍‍`.gitmodules` به فایلها مخزن اصلی اضافه می‌شود. مهم است که این فایل را همانند `.gitignore` به مخزن اضافه کرده تا تاریخچه آن در دسترسی سایرین نیز قرار بگیرد. 

## کار با مخزنی که [submodule] دارد

برای [clone] کردن یک مخزن که دارای یک یا چند [submodule] است دو راه کلی وجود دارد. راه اول بدین شکل است که ابتدا مخزن اصلی [clone] شود و بعد از آن [submodule]ها [clone] شود. در مدل دوم با یک دستور مخزن اصلی و تمامی [submodule]ها یکجا [clone] می‌شود.

در مدل اول ابتدا مخزن [clone] می‌شود:

```bash
$ git clone https://github.com/chaconinc/MainProject
Cloning into 'MainProject'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 14 (delta 1), reused 13 (delta 0)
Unpacking objects: 100% (14/14), done.
Checking connectivity... done.
```
برای [clone] کردن زیر مخزن‌ها به شکل زیر عمل می‌شود:

```bash
$ git submodule init
Submodule 'DbConnector' (https://github.com/chaconinc/DbConnector) registered for path 'DbConnector'
$ git submodule update
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
Submodule path 'DbConnector': checked out 'c3f01dc8862123d317dd46284b05b6892c7b29bc'
‍‍‍```

در مدل دوم با استفاده از تنها یک دستور کل مخزن و زیرمخزن‌ها [clone] می‌شود:

‍‍```bash
$ git clone --recursive https://github.com/chaconinc/MainProject
Cloning into 'MainProject'...
remote: Counting objects: 14, done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 14 (delta 1), reused 13 (delta 0)
Unpacking objects: 100% (14/14), done.
Checking connectivity... done.
Submodule 'DbConnector' (https://github.com/chaconinc/DbConnector) registered for path 'DbConnector'
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
Submodule path 'DbConnector': checked out 'c3f01dc8862123d317dd46284b05b6892c7b29bc'
‍‍‍```

##نکات قابل توجه هنگام استفاده از [submodule]ها
همانطور که در مورد تمام ابزارهای تکنولوژیک صدق می‌کنید هریک از این ابزارها علاوه بر حل کردن مشکلاتی، ممکن است پیچیدگی‌هایی را ایجاد کنند. [submodule]ها هم از این قاعده مستثنا نیستند. مهم‌ترین اتفاق این است که روند کاری پیچیده شده و شما برای هریک کارهای عادی که با مخزنتان انجام می‌دادید حال بایستی بیشتر فکر کنید. در این بخش از نوشته سعی می‌شود با قوانینی به شما برای تصمیم گیری این که چه کاری بایستی انجام شود کمک کند. قطعا این قوانین کامل نبود و عاری از اشکال نیست.

- اگر بخواهید [branch] یکی از [submodule] را عوض کنید کافی است به آن شاخه رفته و با آن به شکل یک مخزن عادی رفتار کرده و [branch] را عوض کنید. 
- برای گرفتن تغییرات [submodule]ها کافی است از `git submodule update --remote` استفاده کنید همچنین این دستور سوئیچ‌های `--merge` و `--rebase` را پشتیبانی می‌کند.
- برای [push] کردن تغییرات بایستی اول [submodule]ها را [commit] کرده و آنها رو [push] کنید و در انتها همین کار را برای مخزن اصلی انجام دهید
- میتوانید از دستور `git submodule foreach` برای اجرای یک دستور خاص روی تمام [submodule]ها استفاده کنید. 
- تغییر [branch] در مخزن اصلی معمولا باعث گیج شدن می‌شود که بایستی ابتدا [submodule] را در [branch] اول ایجاد کرده و فایلها را در [branch] جدید اضافه کنید. برای رفع این مشکل می‌توانید در [branch] جدید از دستور `git submodule update --init` استفاده کنید.
- حذف [submodule] با دستور ‍‍`git submodule rm` انجام می‌شود.

## منابع و خواندن بیشتر
منابع این متن در زیر آمده است:

-[فصل مرتبط] این موضوع در مستندات [git]
- این [پست وبلاگی] که به توضیح تجربه واقعی استفاده پرداخته.

[git]:https://en.wikipedia.org/wiki/Git_(software)
[submodule]:https://git-scm.com/docs/git-submodule
[clone]:http://git-scm.com/docs/git-clone
[branch]:https://git-scm.com/docs/git-branch
[push]:https://git-scm.com/docs/git-push
[commit]:https://git-scm.com/docs/git-commit
[فصل مرتبط]:https://git-scm.com/book/en/v2/Git-Tools-Submodules
[پست وبلاگی]:https://chrisjean.com/git-submodules-adding-using-removing-and-updating/
