اینم یه تجربه پراکنده دیگه!

من قبلا هم در مورد ابزارهایی مثل [makefile] و [cmake] که کامپیال کردن نرم‌افزارها بالاخص در زبان‌های C/C++ رو راحت می‌کنن نوشتم. البته باید بگم که هیچوقت بصورت کامل و درستی یاد نگرفتم که [makefile] چطوره و چطور میشه باهاش سرو کله زد تا اینکه در یکی از پروژه‌ها مجبور به استفاده از [makefile] شدم و با کمک یکی از دوستان یه [پروژه متن‌باز] پیدا کرد که یه مدل آماده [makefile] که توش تقریبا همه کارهای معمول انجام شده بود رو آورده بود.

توی این پست سعی درام که این [پروژه متن‌باز] رو معرفی کنم. خب اول باید بگم که شما برای هر پروژه جدید نیاز دارید که چندتا چیز رو مشخص کنید

1. اینکه بدونید سورس پروژه کجاست.
2. اینکه فولدرهایی که header ها توش قرار گرفته کجاست
3. اینکه بدونید برنامه‌تون به چه کتابخانه‌هایی نیاز داره
4. اینکه بدونید برنامه‌تون برای کامپیال شدن به کمک [GCC] به چه [flag]هایی نیاز داره.

بعد از اینکه این موارد رو دونستید و اونها رو پیدا کردید باید برید و بخشها مرتبط با این موارد رو توی [makefile] تغییر بدید به عنوان Customizable Section مشخص شده.

	## Customizable Section: adapt those variables to suit your program.
	##==========================================================================

	# The pre-processor and compiler options.
	MY_CFLAGS =

	# The linker options.
	MY_LIBS   =

	# The pre-processor options used by the cpp (man cpp for more).
	CPPFLAGS  = -Wall

	# The options used in linking as well as in any direct use of ld.
	LDFLAGS   =

	# The directories in which source files reside.
	# If not specified, only the current directory will be serached.
	SRCDIRS   =

	# The executable file name.
	# If not specified, current directory name or `a.out' will be used.
	PROGRAM   =

خب هر یک از این بخش‌های قابل تغییر برای خودش معنایی داره

1. بخش `MY_CFLAGS` مقدار [flag] هایی هست که برای کامپیال کردن فایلها با پسوند c به کار میره. لازه به ذکره که بدونید [flag]های C با C++ می‌تونن تفاوت اساسی داشته باشند
2. بخش `MY_LIBS` نشون‌دهنده [flag] هایی هست که در فاز [link] قرار به [linker] داده بشه و با استفاده از اون کتابخانه ها شناسونده بشن. یه مثال برای این مقدار `-lpthread` هست که میگه کتابخانه `pthread` مورد نیاز این نرم‌افزار هست
3. بخش `CPPFLAGS` بخشی هست که نشون میده [flag]های کامپایل c++ چیا هستن. مثلا `-std=gnu++11` که نشون میده میخوایم از استاندارد [C++ 2011] استفاده کنیم. فولدر headerها رو هم توی این بخش اضافه می‌کنیم
4. اگه به هر دلیل بخوایم [flag]های دیگه ای به [linker] بدیم از `LDFLAGS` استفاده می‌کنیم.
5. سورس نرم‌افزار رو با `SRCDIRS` جاهایی که سورس قرار گرفته رو نشون میده.
6. و در نهایت `PROGRAM` نام نرم‌افزار رو نشون میده.

امیدوارم با این توضیحات کوتاه دستتون اومده باشه که چه کاری رو به چه صورت باید انجام بدید و در صورت هرگونه سوالی کامنت بگذارید و یادتون نره که من هنوز [makefile] رو بخوبی بلد نیستم! ;)
[makefile]:https://en.wikipedia.org/wiki/Makefile
[cmake]:https://en.wikipedia.org/wiki/CMake
[GCC]:https://en.wikipedia.org/wiki/GNU_Compiler_Collection
[flag]:https://en.wikipedia.org/wiki/Parameter_(computer_programming)#Parameters_and_arguments
[link]:https://en.wikipedia.org/wiki/Linker_(computing)
[linker]:https://en.wikipedia.org/wiki/Linker_(computing)
[C++ 2011]:https://en.wikipedia.org/wiki/C%2B%2B11
[پروژه متن‌باز]:https://sourceforge.net/projects/gcmakefile/
