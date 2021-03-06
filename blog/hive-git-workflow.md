یکی از مهم‌ترین سوالاتی که برای شخص من پس از آشنایی با [git] و ذات توزیع شده آن ایجاد شد این بود که چگونه می‌توان در محیط شرکت و پروژه‌های شخصی از این ابزار به خوبی استفاده کرد؟ برای پاسخ دادن به این سوال منم در آن زمان تحقیقاتی انجام دادم که نتیجه آنها این روندهای کار است که اینجا ارائه می‌شود.

## روند کاری متمرکز

در این روند از [git] همانند یک راه‌حل مدیریت نسخه متمرکز(مانند subversion) استفاده می‌شود. بدین صورت که تنها یک [مخزن] کد وجود داشته که تمامی توسعه‌دهندگان از آن استفاده می‌کنند. بدین صورت که تمامی آنها از این مخرن یک [clone] داخلی بوجود آورده و روی آن کار می‌کنند. آنها تغییرات مورد نیاز خود را روی کد اعمال کرده و آنها را [commit] می‌کنند. سپس این تغییرات را به سرور مرکزی ارسال می‌کنند. ممکن است در این حالت تغییر دو توسعه دهنده با یکدگیر در تضاد بوده یا به اصلاح [conflict] رخ دهد. در این حالت آن دو بایستی با یکدیگر همکاری نموده و مشکل را رفع کنند. 

## روند کاری شاخه ویژگی‌ها

در این روند کاری به ازای هریک از ویژگی‌ها نرم‌افزار یک [شاخه] مجزا بجای master تولید شده و توسعه در آن به پایان رسیده و مورد تست قرار می‌گیرد. نتیجه این کار این است که توسعه دهندگان مختلف می‌توانند بدون نگرانی ویژگی‌ها را بطور همزمان انجام داده و به نتیجه برسانند. همچنین این کار باعث می‌شود که شاخه master همیشه حاوی کد سالم باشد. همچنین در این روش می‌توان از [pull request] نیز استفاده کرد. حسن استفاده از [pull request] امکان همکاری، بحث و بازبینی کد توسط سایر توسعه دهندگان است. همچنین توصیه می‌شود که شاخه‌ها در این روند کار بسیار کوچک و متمرکز باشند. به عنوان مثلا برای رفع مشکل ۲۳۵ باشد. 

### [pull request]

وقتی یکی از توسعه دهندگان کار را به اتمام رساند بجای [merge] کردن فوری کد در master، او آن شاخه را به سرور فرستاده و یک [pull rquest] را ایجاد می‌کند. این باعث می‌شود که سایر توسعه دهندگان بتوانند کد او را بررسی کرده و در صورتی تایید توسط آنها این کد به کد اصلی اضافه شود. همچنین می‌توان از این ويژگی قبل از اتمام یک ویژگی و در حین آن به منظور گرفتن راهنمایی یا بازخورد اولیه از سایر توسعه دهندگان استفاده کرد. 

بعد از اتمام بررسی کد عملیات ادغام کد با master انجام شده و نتیجه به مخزن ارسال می‌گردد. 

## روند کاری Gitflow

این روند توسط آقای [وینسنت دریسن] پیشنهاد و مورد پذیرش جامعه کاربری قرار گرفته است. این روند دستور یا عملیات جدید به روند کاری شاخه ویژگی‌ها اضافه نمی‌کند بلکه به هر شاخه مفهوم و کارکرد خاصی اختصاص داده و براساس کارکرد و مفهوم آنها را دستکاری کرده یا ادغام می‌کند. علاوه بر شاخه‌های هر یک از ویژگی‌ها، در این روند شاخه‌هایی برای ایجاد، نگهداری و آرشیو هریک از نسخه‌های برنامه ایجاد می‌کند. در این روش دو شاخه اصلی وجود برای تاریخچه نرم‌افزار وجود دارد. یکی همان شاخه master و دیگری شاخه‌ای به نام Develop است. شاخه Develop جایی است که تمامی ویژگی‌ها با یکدیگر ادغام می‌شوند. همچنین در شاخه master با استفاده [tag]ها نسخه‌های مختلف نرم‌افزار از یکدیگر مجزا می‌شوند. 

در این روش شاخه یک ویژگی جدید بجای اینکه از master بوجود بیاید از Develp بوجود آمده و در نهایت در Develop ادغام می‌شود. پس از اجتماع ویژگی‌ها کافی در شاخه Develop شاخه‌ای به نام Release از شاخه Develop ایجاد شده که دیگر ویژگی‌جدیدی به آن اضافه نخواهد شد، بلکه تنها عملیات مرتبط با انتشار نسخه شامل بهبود مستندات، رفع باگ و ... روی آن انجام خواهد شد. پس نهایی شدن شاخه Release این شاخه در master اداغام شده و با یک شماره نسخه [tag] میشود. همچنین این شاخه درون Develop نیز ادغام خواهد شد. 

همچنین شاخه‌ای به نام Maintenace بایستی برای رفع باگ‌های حیاتی ایجاد شود. این شاخه حتما از master ایجاد شده و دوباره در master ادغام می‌شود. پس از ادغام بایستی ورژن مربوطه نیز بصورت [tag] به master اضافه شود. 

## روند کاری منشعب

این روند کاری اساسا با روندهای کاری ارائه شده تاکنون متفاوت است. بدین معنا که در روندهای قبل تنها یک مخزن سمت سرور وجود داشته که توسعه دهندگان تغییرات خود را روی آن اعمال می‌کردند. در این روش یک مخزن کد به ازای هریک از توسعه‌دهندگان وجود دارد. مهمترین ویژگی این روش این است که ویژگی‌ها می‌توانند بدون نیاز به ارسال تغییرات به سرور از سوی تمامی افراد انجام شود. در این حالت توسعه دهندگان تغییرات خود را به مخزن خود در سرور ارسال می‌کنند. همچنین نگهدارنده پروژه تنها اجازه تغییر مخزن اصلی پروژه را دارد. این حالت باعث می‌شود که نگهدارنده پروژه بتواند تک تک تغییرات آنها را بپذیرد یا رد کند. در این حالت توسعه دهندگان به مخزن اصلی کد دسترسی نوشتن ندارند. این حالت باعث می‌شود که انعطاف پذیری کافی برای تیم‌های بزرگ با ساختار گروهی نامشخص ایجاد شود. همچنین این روش مناسب حالتی است که به توسعه‌هندگان اعتماد کافی وجود ندارد. این روش بیشتر در پروژه‌های متن‌باز مورد استفاده قرار می‌گیرد. 

روش کار در این روند بدین صورت است که به هر توسعه دهنده جدید ابتدا از مخزن کد یک انشعاب به نام خود روی سرور ایجاد می‌کند. پس از انجام تغییرات و نهایی شدن آنها، تغییرات را روی مخزن خود اعمال کرده و یک [pull request] جدید می‌سازد. پس از ایجاد درخواست و بررسی کد در صورت تایید شدن تغییرات توسط نگهدارنده کد، آن تغییرات در مخزن اصلی پروژه وارد می‌شود. پس اعمال این تغییرات هریک از توسعه دهندگان بایستی مخازن خود را با مخزن اصلی sync کنند. لازم به ذکر است که در این روش مخزن اصلی پروژه یک مفهوم قراردادی است و میان مخزن اصلی پروژه و مخزن هریک از کاربرها از نظر فنی هیچ تفاوتی وجود ندارد. 

در این روش همه توسعه دهندگان و نگهدارنده پروژه از روندهای قبلی در مخازن خود و مخزن اصلی برنامه استفاده می‌کنند. تنها تفاوت این است که شاخه‌ها در این روش به مخزن هریک توسعه دهندگان بجای مخزن اصلی ارسال می‌شود. 

## منابع و مطالعه بیشتر

- [منبع اول]
- [منبع دوم]
- [منبع سوم]
- [منبع چهارم]



[git]: https://en.wikipedia.org/wiki/Git_(software)
[pull request]:http://git-scm.com/docs/git-request-pull
[tag]:https://git-scm.com/book/en/v2/Git-Basics-Tagging
[merge]:http://git-scm.com/docs/git-merge
[clone]:http://git-scm.com/docs/git-clone
[وینسنت دریسن]:http://nvie.com/posts/a-successful-git-branching-model/	
[شاخه]:https://git-scm.com/ref/git-branch
[مخزن]:https://en.wikipedia.org/wiki/Repository_%28revision_control%29
[منبع اول]:https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow
[منبع دوم]:http://nvie.com/posts/a-successful-git-branching-model/
[منبع سوم]:https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows
[منبع چهارم]:https://sandofsky.com/blog/git-workflow.html

