# آموزش ایجاد قالب (Template) در ویژوال استودیو

وقتی از لایه بندی و معماری در پروژه خودمون استفاده کنیم، به خصوص استفاده از معماری مانند DDD و مایکروسرویس که ما برای ایجاد هر سرویس نیاز به ایجاد ساختار و انجام یکسری کار تکراری داریم میتوانیم با استفاده از قابلیتی که در ویژوال استودیو ایجاد شده است استفاده کنیم و از انجام کارهای تکراری مثل ساخت پروژه ها، پوشه بندی، ایجاد فایل های اولیه، تنظیمات و ... اجتناب کنیم و همچنان به اصول اولیه نرم افزار از جمله اصل DRY پایبند باشیم.

این قالب میتواند یک یا چند پروژه باید. در این مثال ما با ایجاد ساختار کامل از جمله solution به همراه چند پروژه ایجاد میکنیم تا بتوانیم نیاز های خودمون رو برطرف کنیم.

 برای این مثال ما یک پروژه داریم که حاوی صفحه وب میباشد و یک پروژه دیگر که کانفیگ درون آن وجود دارد. صرفا به لحاظ ارتباط و استفاده از آبجکت های پروژه دیگر میباشد و قطعا در مثال های بیشتر قابل بسط دادن میباشد.

برای ایجاد قالب ابتدا به چند پروژه نیاز داریم که به صورت زیر ایجاد میکنیم
1. یک پروژه به صورت `ASP.NET Core Web App` ایجاد میکنیم
2. یک پروژه به صورت `Class Library` ایجاد میکنیم.

![image](https://user-images.githubusercontent.com/6535038/181941476-47fad449-f85c-4484-b70c-fa5eb44378ac.png)
