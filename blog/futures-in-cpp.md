اینم یه تجربه پراکنده دیگه!

خب من به مسائل مرتبط با کارایی و اجرای غیر همزمان کدها یا همون [async] رو دوست دارم. یکم هم تجربه کد نویسی رو باهاشون دارم. توی این پست میخوام بصورت ساده یکی از روشهای این پیاده‌سازی رو براتون توضیح بدم. خیلی دنبال این نیستم که بگم دقیقا این روش کجاها به درد میخوره و چرا به درد میخوره بلکه هدف یه معرفی اولیه است. انشالا در یه پست مفصل بیشتر توضیح میدم.

کل موضوع حول دوتا واژه [promise] و [future] میگرده که در [c++0x11] معرفی شده. داستان از این قراره که در مدل [sync] شما یه تابع رو صدا میزنی و منتظر میمونی که جواب به شما برگرده. اما در این مدل بعد از صدا زدن یک تابع بجای منتظر موندن برای جواب همون موقع یک مقدار از نوع [future] برمیگرده که تا زمانی که تابع صدا زده شده به اتمام نرسیده مقداری نداره. بعد از تموم شدن تابع مقدار [future] همون مقداری هست که نتیجه محاسباته. حالا اگه از منظر تابعی که صدا زده میشه نگاه کنیم اون تابع خروجیش از نوع [promise] هست که بعد از اتمام اون رو پر میکنه و برمیگردونه. همین!

حالا این نمونه کد رو هم ببنید که یه مثال ساده از [future] و [promise] هست. 

مثالها از [اینجا] گرفته شده. اولین مثال از این قرار که ما یه تابع که خروجیش void هست رو با استفاده [future] مورد استفاده قرار می‌دیم.

```c++
#include <future>
#include <iostream>

void called_from_async() {
  std::cout << "Async call" << std::endl;
}

int main() {
  //called_from_async launched in a separate thread if possible
  std::future<void> result( std::async(called_from_async));

  std::cout << "Message from main." << std::endl;

  //ensure that called_from_async is launched synchronously
  //if it wasn't already launched
  result.get();

  return 0;
}
```
اتفاقی که اینجا میفته اینه که با استفاده از ‍`std::async` ما سعی میکنیم که اون تابع رو در یک [thread] دیگه اجرا کنیم و نتیجه رو بصورت یک [future] از اون بگیریم. با اجرای `result.get()` مطمئن می‌شیم که اجرای اون [thread] به اتمام رسیده.

مثال دوم یه محاسبه بصورت غیر همزمان اجرا میشه و نتیجش به کمک [future] برگردونده میشه

```
#include <future>
#include <iostream>
#include <vector>

int twice(int m) {
  return 2 * m;
}

int main() {
  std::vector<std::future<int>> futures;

  for(int i = 0; i < 10; ++i) {
    futures.push_back (std::async(twice, i));
  }

  //retrive and print the value stored in the future
  for(auto &e : futures) {
    std::cout << e.get() << std::endl;
  }

  return 0;
}
```

امیدوارم که این بدردتون خورده باشه.
همین!
[اینجا]:https://solarianprogrammer.com/2012/10/17/cpp-11-async-tutorial/ 
[async]:https://en.wikipedia.org/wiki/Asynchrony
[promise]:https://en.wikipedia.org/wiki/Futures_and_promises
[future]:https://en.wikipedia.org/wiki/Futures_and_promises
[c++0x11]:https://en.wikipedia.org/wiki/C%2B%2B11
[sync]:https://en.wikipedia.org/wiki/Synchronization 
[thread]:https://en.wikipedia.org/wiki/Thread_(computing)


[1]: https://github.com/facebook/folly/tree/master/folly/futures
[2]: https://twitter.github.io/finagle/guide/Futures.html
[3]: https://news.ycombinator.com/item?id=9746405
[4]: https://en.wikipedia.org/wiki/Futures_and_promises#Read-only_views
[5]: http://instagram-engineering.tumblr.com/post/121930298932/c-futures-at-instagram

