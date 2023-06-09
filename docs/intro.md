# مقدمه


یک غذای خوشمزه مثل قرمه‌سبزی را در نظر بگیرید. حتما تا به حال قرمه‌سبزی‌های زیادی خوردید که ممکن است آشپزهای یکسان یا غیریکسانی داشته باشند. آیا مزه تمامی آن‌ها یکسان بوده است؟ قطعا تا به حال شده که دو بار با یک دستور پخت قرمه‌سبزی بپزید ولی مزه‌های یکسان ندهند. قطعا مواد غذایی متفاوت تاثیرگذار است، ولی آیا شما همه دستورات را در دو سری یکسان انجام می‌دهید؟ برای مثال کافی است در یکی از بارهایی که غذا می‌پزید، نمک بیشتری در غذا بریزید تا مزه‌های دو سری متفاوت شود.

حال فرض کنید که یک ماشین غذاپزی ساخته‌ایم که می‌توانیم دستور پخت قرمه‌سبزی را به آن بدهیم و از این موضوع مطمئن باشیم که هر بار دستور پخت یکسان انجام می‌شود و اگر بهترین دستور پخت را داشته باشیم، همیشه بهترین قرمه‌سبزی ممکن را نوش جان می‌کنیم. 

حالا فکر کنید که یک اکانت در یک سایت زیرساخت ابری مثل 
aws
خریداری کردید و می‌خواهید
[VPC](https://en.wikipedia.org/wiki/Virtual_private_cloud)،
Subnet،
گروه امنیتی و
در آخر یک ماشین بسازید که همه بهم مرتبط هستند. برای این‌کار باید مسیر زیر را طی کنید.

1. وارد صفحه خود در AWS Management Console شوید.
2. به منوی VPC dashbord حرکت کنید.
3. روی "Create VPC" کلیک کنید و CIDR block مربوط به VPC خود را وارد کنید.
4. به بخش Subnets بروید و روی "Create Subnet" کلیک کنید.
5. محتویات CIDR block را کامل کنید و VPC ساخته شده را انتخاب کنید.
6. به بخش "Security Groups" بروید و روی "Create Security Group" کلیک کنید.
7. نام و توضیحاتی برای گروه امنیتی خود وارد کنید و VPC ساخته شده را انتخاب کنید.
8. قوانین ورودی و خروجی را به دلخواه اضافه کنید.
9. به EC2 dashboard بروید.
10. روی "Launch Instance" کلیک کنید و AMI مورد نظر خود را انتخاب کنید.
11. یک نوع instance انتخاب کنید و تنظیمات دیگر را به دلخواه تنظیم کنید.
12. در بخش "Configure Security Group"، روی "Select an existing security group" کلیک کنید و گروه امنیتی ساخته شده را انتخاب کنید.
13. ماشین خود را راه‌اندازی کنید.

خب فکر کنید که یکم کارهای بیش‌تری بخواید بکنید. هر بار که یک ماشین جدید می‌خواهید بسازید، همه این فرآیند رو باید طی کنید. یا فکر کنید که چنین کار سختی رو انجام دادید و دفعه بعدی، یکی از همکارانتان می‌خواست دقیقا همان کار شما را انجام بدهد. روشی می‌شناسید که این فرآیند را خودکار بکند؟ 