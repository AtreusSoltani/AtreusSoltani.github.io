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
6. به بخش "Security Groups" بروید ...

(جواب اصلی اینه:)

1. Log in to the AWS Management Console.
2. Navigate to the VPC dashboard.
3. Click on "Create VPC" and enter the CIDR block for your VPC.
4. Navigate to the "Subnets" section and click on "Create subnet".
5. Enter the CIDR block for your subnet and select the VPC you created earlier.
6. Navigate to the "Security Groups" section and click on "Create security group".
7. Enter a name and description for your security group, and select the VPC you created earlier.
8. Add inbound and outbound rules as desired.
9. Navigate to the EC2 dashboard.
10. Click on "Launch Instance" and select the AMI you want to use.
11. Choose the instance type and configure other settings as desired.
12. In the "Configure Security Group" section, select "Select an existing security group" and choose the security group you created earlier.
13. Launch your instance.

خب فکر کنید که یکم کارهای بیش‌تری بخواید بکنید. هر بار که یک ماشین جدید می‌خواهید بسازید، همه این فرآیند رو باید طی کنید. یا فکر کنید که چنین کار سختی رو انجام دادید و دفعه بعدی، یکی از همکارانتان می‌خواست دقیقا همان کار شما را انجام بدهد. روشی می‌شناسید که این فرآیند را خودکار بکند؟ 