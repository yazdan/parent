اینم یه تجربه پراکنده دیگه!

همانطور که میدونید من اخیرا کتاب [پیش‌نمونه‌سازی] رو ترجمه کردم. کلی چیزهای مفید در راه این ترجمه یاد گرفتم. حالا به پیشنهاد [جادی] سراغ این رفتم که نسخه [epub] این کتاب رو هم ایجاد کنم تا آدم‌های بیشتری بتونن راحت‌تر بخوننش و ازش استفاده کنن. همچنین باید بگم که [جادی] زحمت کشیده توی [لینک‌های شاد دوشنبه آخر ماه] این کتاب رو معرفی کرده.

کلا هم بخاطر وجود ابزار بسیار خوبی به اسم [pandoc] و نوشته شدن متن به فرمت [markdown] این عملیات تقریبا راحته!

مراحل این کار بصورت خلاصه اینهاست:

1. اول از همه نوشتن متادیتاهای کتاب توی یک فایل خاص به اسم title.txt به فرمت [yaml]. این متا دیتا شامل اسم کتاب نام نویسنده و این دست اطلاعات است.
2. تهیه کردن یک [css] برای تعیین فونت متن. لازم میدونم که اضافه کنم که [epub] یه فرمت خاص از [xhtml] و [css] یه سری متادیتای دیگه‌است که بصورت فشرده شده ارائه می شه. [css] بوسیله این سوئیج epub-stylesheet به [pandoc] معرفی می‌شه.
3. اضافه کردن فونت‌ها درون فایل [epub] تا در صورتی که فایل روی خواننده مقصد وجود نداشته باشه از این فونت‌ها استفاده بشه. فرمت فونت‌هایی که بصورت رسمی پشتیبانی میشه oft و woff هست. اما استفاده از ttf و تقریبا سایر فرمت‌های فونت‌های وب هم پشتیبانی می‌شه. [pandoc] این کار رو با سوئیچ epub-embed-font انجام میده.
4. اضافه کردن نحوه ورق خوردن کتاب که از راست به چپ باشه. این کار با کلید page-progression-direction توی متادیتای کتاب در فایل title.txt انجام می‌شه.
5. برای اینکه متن‌ها هم چپ به راست باشن بایستی به تگ ‍‍‍‍‍‍`<html>` هریک از بخشها یک ویژگی `dir="rtl"` اضافه بشه. اینکار بصورت مستقیم قابل انجام نبود و به همین خاطر با رجوع به میلینگ لیست [pandoc] و پرسیدن در این مورد با استفاده از چیزی به اسم template این مشکل هم حل شد.

نمونه انجام این کار توی [شاخه epub] تو [github] کتاب قابل روئیته.

همین!
[پیش‌نمونه‌سازی]: http://pretotyping.ir
[جادی]: http://jadi.net
[لینک‌های شاد دوشنبه آخر ماه]:http://jadi.net/2015/07/mondays-tir-2/
[شاخه epub]: https://github.com/yazdan/pretotypeit/tree/epub

[epub]: https://en.wikipedia.org/wiki/EPUB
[pandoc]: https://msdn.microsoft.com/en-us/library/ms930369.aspx
[markdown]: http://daringfireball.net/projects/markdown/
[yaml]:https://en.wikipedia.org/wiki/YAML
[css]:https://en.wikipedia.org/wiki/Cascading_Style_Sheets
[xhtml]:https://en.wikipedia.org/wiki/XHTML
[github]:https://github.com/yazdan/pretotypeit


