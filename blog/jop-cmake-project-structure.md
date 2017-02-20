اینم یه تجربه پراکنده دیگه!

متاسفانه یه مدت میشه که سرم بیش از اندازه شلوغ شده و نرسیدم وبلاگ بنویسم.  [قبلا] در مورد [cmake] نشوتم و حالا خواستم یکم بیشتر بنویسم. 

خب توی این پست سعی میکنم که بگم که توی دنیای واقعی من از [cmake] چطور میتونم استفاده کنم. توی دنیای واقعی معمولا پروژه از این بخش‌ها تشکیل شده:

1. یه سری سورس که اصل منطق برنامه اونجا پیاده سازی شده
2. یه فایل اصلی یا main که تابع اصلی نرم افزار اونجا قرار گرفته
3. احتمالا یه سری تست که نرم افزار رو بصورت اتوماتیک مورد تست قرار میدن
4. احتمالا یه سری کتابخانه که بصورت [static] یا [dynamic] به کد اضافه میشن.

یه خورده توضیح بدم که توی م[cmake] معمولا یه چیزی داریم به عنوان خروجی که میتونه از جنس فایل اجرایی باشه یا از جنس کتابخانه. ما با ترکیب کتابخانه‌ها و سورس کدهای موجود فایل اجرایی نهایی رو درست میکنیم. روند کار هم معمولا به این صورته که:
1. سورسهای اصلی بصورت یه کتابخانه [static] کامپایل میشه
2. فایل اصلی برنامه بصورت یک فایل اجرایی کامپایل شده و به کتابخانه سورس‌های اصلی لینک میشه
3. تست کیسها بصوت یک فایل اجرایی کامپایل شده و به کتابخانه سورس‌هاس اصلی لینک میشه.
4. کتابخانه ها هم به فایل اجرایی اضافه میشن.

حالا اگه مثال بخوایم یه پروژه رو مثال بزنم که ساختار کدش به شکل زیره

	inc/
	 +-------- utility.h
	src/
	 +-------- utility.c
	 +-------- main.c
	tst/
	 +-------- main.c

فایل [CMakeLists.txt] این پروژه یه چیزی شبیه این خواهد بود

	PROJECT(abyz-cmake-test)

	CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

	INCLUDE_DIRECTORIES("${CMAKE_SOURCE_DIR}/inc")

	SET(appLib_src
	    src/utility.c
	  )
	ADD_LIBRARY(applibstatic
	    STATIC
	    ${appLib_src}
	  )
	ADD_EXECUTABLE(abyz-cmake-test
	    src/main.cpp
	  )
	TARGET_LINK_LIBRARIES(abyz-cmake-test
	    applibstatic
	  )
	ADD_EXECUTABLE(unittester
	    tst/main.c
	  )

	TARGET_LINK_LIBRARIES(unittester
	    applibstatic
	  )
شامل یک کتابخانه [static] و دو فایل اجرایی یکی اصل برنامه و دیگری تست برنامه.

همین!

[cmake]: http://cmake.org
[make]: https://en.wikipedia.org/wiki/Make_(software)
[static]:https://en.wikipedia.org/wiki/Static_library
[dynamic]:https://en.wikipedia.org/wiki/Dynamic_linker
[CMakeLists.txt]:https://en.wikipedia.org/wiki/CMake

[قبلا]:http://blog.abyz.ir/1394/04/jop-cmake-introduction/

