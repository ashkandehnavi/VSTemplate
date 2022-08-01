# آموزش ایجاد قالب (Template) در ویژوال استودیو

وقتی از لایه بندی و معماری در پروژه خودمون استفاده کنیم، به خصوص استفاده از معماری مانند DDD و مایکروسرویس که ما برای ایجاد هر سرویس نیاز به ایجاد ساختار و انجام یکسری کار تکراری داریم میتوانیم با استفاده از قابلیتی که در ویژوال استودیو ایجاد شده است استفاده کنیم و از انجام کارهای تکراری مثل ساخت پروژه ها، پوشه بندی، ایجاد فایل های اولیه، تنظیمات و ... اجتناب کنیم و همچنان به اصول اولیه نرم افزار از جمله اصل DRY پایبند باشیم.

این قالب میتواند یک یا چند پروژه باید. در این مثال ما با ایجاد ساختار کامل از جمله solution به همراه چند پروژه ایجاد میکنیم تا بتوانیم نیاز های خودمون رو برطرف کنیم.

 برای این مثال ما یک پروژه داریم که حاوی صفحه وب میباشد و یک پروژه دیگر که کانفیگ درون آن وجود دارد. صرفا به لحاظ ارتباط و استفاده از آبجکت های پروژه دیگر میباشد و قطعا در مثال های بیشتر قابل بسط دادن میباشد.

## ساخت پروژه ها

برای ایجاد قالب ابتدا به چند پروژه نیاز داریم که به صورت زیر ایجاد میکنیم

1. یک پروژه به صورت `ASP.NET Core Web App` به نام `Dashboard.API` ایجاد میکنیم
2. یک پروژه به صورت `Class Library` به نام `Dashboard.Data` ایجاد میکنیم

![image](https://user-images.githubusercontent.com/6535038/181941476-47fad449-f85c-4484-b70c-fa5eb44378ac.png)

مرحله بعد از پروژه `Dashboard.API` به پروژه `Dashboard.Data` رفرنس میدهیم.

در فایل `DashboardConfigs.cs` ساخته شده در پروژه `Dashboard.Data` به صورت زیر عمل میکنیم

    namespace Dashboard.Data
    {
        public static class DashboardConfigs
        {
            public static string AppTitle = "This is Dashboard Project";
        }
    }

در فایل `index.cshtml` در پروژه `Dashboard.API` نیز کد زیر را جایگزین میکنیم

    @page
    @model IndexModel
    @{
        ViewData["Title"] = "Home page";
    }

    <div class="text-center">
        <h1 class="display-4">@Dashboard.Data.DashboardConfigs.AppTitle</h1>
    </div>

به این ترتیب وقتی ما صفحه وب را در API لود کنیم مقداری که در کانفیگ پروژه Data ست کردیم نمایش میشود.

فرض کنید ما این ساختار را باید برای هر مایکروسرویس خود پیاده کنیم و نام کلاس ها، فیلد ها، پروپرتی ها، مقادیر و ... را هربار تکراری ایجاد کنیم واقعا کاری طاقت فرساست (😥) اینجاست که ساخت قالب به کمکمون میاد و میتونه خیلی ازین کارهای تکراری رو واسمون حل کنه.

## خروجی گرفتن قالب از پروژه

برای این کار وقتی در ویژوال استودیو هستیم و solution رو باز کردیم، از منوی بالا گزینه `Project > Export Template` رو انتخاب میکنیم

![image](https://user-images.githubusercontent.com/6535038/182029782-da2c0584-2cf8-4612-824c-813d04612319.png)

یک پنچره مانند پنجره پایین باز میشود

![image](https://user-images.githubusercontent.com/6535038/182029900-2bb0c1b6-1feb-47e7-880f-8f345142248f.png)

در حال حاضر ما گزینه `Project template` رو انتخاب میکنیم(اون یکی رو بعدا ایشالا توضیح میدم) و در قسمت پایین نام پروژه مون رو انتخاب میکنیم. و به صفحه بعدی میریم.

![image](https://user-images.githubusercontent.com/6535038/182029994-f24a0657-c5b2-4325-b729-6bbcbea8a180.png)

هر دو تیک رو غیر انتخاب میکنیم و گزینه Finish رو کلیک میکنیم.

وقتی این کار رو کنیم در واقع از پروژه انتخابی یک Template ایجاد میشه(که از همین هم میتونیم برای قالب استفاده کنیم و هنگام ایجاد پروژه جدید از این قالب برای ساخت پروژه استفاده کنیم)

مسیر خروجی قالب ها در ویندوز به این صورت هست:

    C:\Users\<Your_User>\Documents\Visual Studio 2022\My Exported Templates\

برای هر دو پروژه این مراحل رو طی میکنیم تا دو فایل زیپ شده در مسیر بالا قرار گیرد.

- Dashboard.API.zip
- Dashboard.Data.zip

سپس محتویات هر دو فایل رو در فولدر هایی هم نام خودشون Extract میکنیم.

![image](https://user-images.githubusercontent.com/6535038/182030350-8ad25cba-de16-4362-aeee-91ff50d080f4.png)

## ایجاد فایل &lrm; .vstemplate

حالا نوبت این میرسه که فایل تنظیماتی اضافه کنیم که پروژه هامون به همراه solution برامون ایجاد کنه.
در کنار همین فولدر ها یک فایل به نام `Template.vstemplate` ایجاد میکنیم و محتویات زیر رو درون اون قرار میدیم.

    <VSTemplate Version="2.0.0" Type="ProjectGroup" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <TemplateData>
            <Name>Microservice Template</Name>
            <Description>قالب پیش ساخته برای ایجاد مایکروسرویس</Description>
            <ProjectType>csharp</ProjectType>
        </TemplateData>

        <TemplateContent>
            <ProjectCollection>
                <SolutionFolder Name="src">
                    <ProjectTemplateLink ProjectName="Dashboard.API" CopyParameters="true">Dashboard.API\MyTemplate.vstemplate</ProjectTemplateLink>
                    <ProjectTemplateLink ProjectName="Dashboard.Data" CopyParameters="true">Dashboard.Data\MyTemplate.vstemplate</ProjectTemplateLink>
                </SolutionFolder>
            </ProjectCollection>
        </TemplateContent>
    </VSTemplate>

![image](https://user-images.githubusercontent.com/6535038/182031149-40e135e4-c345-4ac4-8f6f-bdc964f7649b.png)

محتویات تگ `TemplateData‍` به این صورت هست:

- &rlm; Name: نام قالب رو نشون میده
- &rlm; Description: توضیحاتی برای نمایش
- &rlm; ProjectType: نوع پروژه که در اینجا سی شارپ هست

لیست تمام Element هایی که در این تگ میتونه قرار بگیره و قابل تنظیم هست در لینک زیر اومده

[مشاهده لیست تگ ها](https://docs.microsoft.com/en-us/visualstudio/extensibility/templatedata-element-visual-studio-templates?view=vs-2022)

محتویات تگ `TemplateContent` به این صورت هست:


- &rlm; ProjectCollection: برای اینکه لیستی از پروژه ها بتونیم اضافه کنیم باید از این تگ استفاده کنیم
    - &rlm; SolutionFolder: برای اینکه در solution بتوانیم پروژه ها را در یک فولدر قرار دهیم استفاده میکنیم. در اینجا تمام پروژه ها در فولدر src قرار میگیره
        - &rlm; ProjectTemplateLink: این تگ برای لینک کردن به پروژه مورد نظر هست. `ProjectName` نام پروژه ای که در solution قرار میگیره هست و داخل تگ آدرس اون پروژه مسیر دهی میشه

## تولید فایل قالب

در نهایت هر دو فولدر به همراه این فایل تنظیمات رو به صورت zip کرده.

![image](https://user-images.githubusercontent.com/6535038/182031949-b95996a3-3b4e-4898-9c84-53524767cd32.png)

## نصب قالب در ویژوال استودیو

برای نصب این قالب هیچ کار پیچیده ای قرار نیست انجام بدیم فقط فایل zip تولید شده رو کپی کرده و در مسیر زیر قرار میدهیم.

    C:\Users\<Your_User>\Documents\Visual Studio 2022\Templates\ProjectTemplates\Visual C#

وقتی این کار رو انجام بدیم کافیه ویژوال استودیو رو باز کنیم و یک پروژه جدید ایجاد کنیم

![image](https://user-images.githubusercontent.com/6535038/182032234-eb0ce0e8-c0ed-434b-8330-a8b9924c41f1.png)

![image](https://user-images.githubusercontent.com/6535038/182139309-f630bdbe-95b9-4a74-84f6-e900314ae306.png)

![image](https://user-images.githubusercontent.com/6535038/182032304-618a52e9-e686-45b5-a86b-f60a949d7c36.png)

در نهایت همانطور که مشاهده میکنید پروژه به همراه فایل ها و ساختار اون ایجاد شد.

حالا وقت اون رسیده یه پله بالاتر بریم.
قطعا وقتی ما میخواهیم قالب ایجاد کنیم صرفا به ساختار نیاز نداریم و میخواهیم فایل ها و پروژه هامون هم بر اساس نامی که نیاز داریم ایجاد بشه برای این کار میتونیم از قابلیت parameter استفاده کنیم و میخوایم هرجا که از Dashboard استفاده شده جای اون نامی که مد نظر ما هست قرار بگیره. `$ext_safeprojectname$Configs.cs` یکی از parameter هایی هست که ما میتونیم استفاده کنیم و به صورت خودکار با نام پروژه ای که هنگام ایجاد کردن وارد میکنیم، مقدار دهی میشه. برای این کار به این صورت عمل میکنیم:

[لیست کامل parameter ها](https://docs.microsoft.com/en-us/visualstudio/ide/template-parameters?view=vs-2019)

در پروژه `Dashboard.Data` نام فایل `DashboardConfigs.cs` را به `$ext_safeprojectname$Configs.cs` تغییر میدهیم و محتویات آن را به شکل زیر جایگزین میکنیم.

    namespace $ext_safeprojectname$.Data
    {
        public static class $ext_safeprojectname$Configs
        {
            public static string AppTitle = "This is $ext_safeprojectname$ Project";
        }
    }

همینطور فایل پروژه `Dashboard.API` را باز کرده و رفرنس پروژه به `Dashboard.Data` را به صورت زیر تغییر میدهیم:

    <ItemGroup>
        <ProjectReference Include="..\$ext_safeprojectname$.Data\$ext_safeprojectname$.Data.csproj" />
    </ItemGroup>

به همین ترتیب فایل `Index.cshtml` رو به صورت زیر تغییر میدهیم:

    @page
    @model IndexModel
    @{
        ViewData["Title"] = "Home page";
    }

    <div class="text-center">
        <h1 class="display-4">@$ext_safeprojectname$.Data.$ext_safeprojectname$Configs.AppTitle</h1>
    </div>

حالا مجدد فرایند خروجی گرفتن رو که در [این لینک](#خروجی-گرفتن-قالب-از-پروژه) توضیح داده شده رو انجام میدهیم.
نکته ای که هست نیاز این هست که با انجام تغییرات پروژه بیلد نمیشه و این اصلا اهمیت نداره چون ما فقط میخواهیم قالب تولید کنیم.

بعد از اینکه مرحله بالا رو برای پروژه ها انجام دادیم حالا فایل Template.vstemplate رو به صورت زیر تغییر میدهیم:

    <VSTemplate Version="2.0.0" Type="ProjectGroup" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <TemplateData>
            <Name>Microservice Template</Name>
            <Description>قالب پیش ساخته برای ایجاد مایکروسرویس</Description>
            <ProjectType>csharp</ProjectType>
        </TemplateData>

        <TemplateContent>
            <ProjectCollection>
                <SolutionFolder Name="src">
                    <ProjectTemplateLink ProjectName="$safeprojectname$.API" CopyParameters="true">Dashboard.API\MyTemplate.vstemplate</ProjectTemplateLink>
                    <ProjectTemplateLink ProjectName="$safeprojectname$.Data" CopyParameters="true">Dashboard.Data\MyTemplate.vstemplate</ProjectTemplateLink>
                </SolutionFolder>
            </ProjectCollection>
        </TemplateContent>
    </VSTemplate>

با استفاده از `$safeprojectname$` نام پروژه ای که ایجاد میشه در Solution ما بر اساس نام وارد شده ما میشه و به این ترتیب تمام تغییرات اعمال میشه. فقط دقت داشته باشید که مسیر فولدر و نام پروژه رو تغییری ندادیم و نیازی به این کار نیست.

حالا اگر مجدد فرایند [تولید قالب](#تولید-فایل-قالب) و [نصب قالب](#نصب-قالب-در-ویژوال-استودیو) رو انجام بدیم در هنگام ایجاد solution جدید و استفاده از قالب تهیه شده مشاهده میکنیم که فایل ها و مقادیر که مورد نظرمون بود به درستی تغییر پیدا کرده اند.

![image](https://user-images.githubusercontent.com/6535038/182138586-87049715-14c4-42d1-bf18-938c033b490e.png)

![image](https://user-images.githubusercontent.com/6535038/182138780-32e0a8cb-6c11-4740-9004-27bfbd3ac000.png)

![image](https://user-images.githubusercontent.com/6535038/182139518-d03877fc-849a-42b1-8ea5-78785ea9471d.png)

و تمام 😍

## چند تا نکته

این چند تا نکته هم توجه داشته باشید:

1. &rlm;فایل zip خروجی رو به راحتی میتونید روی فایل قبلی که ایجاد کرده بودید replace کنید.
2. &rlm; نسخه ویژوال استودیو من 17 یا 2019 هست.
3. &rlm; کش کردن قالب

ممکن هست وقتی قالب رو تغییر میدهید و مجدد در مسیر قالب ها قرار میدهید تغییرات اعمال هنگام ساخت پروژه جدید مشاهده نشده و درواقع ویژوال استودیو اون رو کش کرده باشه. برای حذف کش به این دو مسیر اشاره شده در زیر برید و محتویات کل فولدر رو حذف کنید و دوباره اقدام به باز کردن ویژوال استودیو و ساخت پروژه کنید

    C:\Users\<Your_User>\AppData\Local\Microsoft\VisualStudio\17.0_af7cf0b1\ProjectTemplatesCache_{00000000-0000-0000-0000-000000000000}

    C:\Users\<Your_User>\AppData\Roaming\Microsoft\VisualStudio\17.0_af7cf0b1\ProjectTemplatesCache

\
\
\
فایل قالب و خروجی در فولدر src قرار داده شده است.
