# ایجاد زیرساخت

بعد از نصب کردن ترافورم، آماده‌اید تا اولین زیرساخت خود را ایجاد کنید.

در این آموزش، یک اینستنس[^1]
EC2
از
Amazon Web Services
(AWS)
تهیه می‌کنید.

## پیشنیازها

* Terraform CLI را نصب کنید.
* AWS CLI را نصب کنید.
* اکانت AWS account که بتوانید با آن منابع را بسازید.

برای اینکه از اطلاعات هویتی خود برای
Terraform AWS Provider
استفاده کنید، مقدار متغیر محلی[^2]
`AWS_ACCESS_KEY_ID`
و
`AWS_SECRET_ACCESS_KEY`
را مقداردهی کنید.

```shell
$ export AWS_ACCESS_KEY_ID=
$ export AWS_SECRET_ACCESS_KEY=
```

!!! Tip
    اگر دسترسی به اکانت
    AWS
    ندارید، از روش‌های دیگر برای احراز هویت که در
    [AWS provider documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#environment-variables)
    است، استفاده کنید.

## فایل‌های پیکربندی

فایل‌هایی که در آن‌ها مشخصات زیرساخت در ترافورم نوشته می‌شود به
`Terraform Configuration`
یا پیکربندی ترافورم معروف است.

هر پیکربندی ترافورم باید در پوشه مربوط به خودش باشد. یک پوشه برای فایل‌های پیکربندی خود بسازید.
```shell
$ mkdir learn-terraform-aws-instance
```

به آن پوشه بروید.
```shell
$ cd learn-terraform-aws-instance
```

یک فایل بسازید که در آن زیرساخت خود را تعریف می‌کنید.
```shell
$ touch main.tf
```

فایل
`main.tf`
را در یک ویرایشگر متن مانند
VSCode
باز کنید و محتوای پیکربندی زیر را در آن قرار دهید.

```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-830c94e3"
  instance_type = "t2.micro"

  tags = {
    Name = "ExampleAppServerInstance"
  }
}
```

این یک پیکربندی کامل است که می‌توانید آن را با ترافورم دپلوی[^3]
کنید.

### terraform

تنظیمات ترافورم در قطعه
`terraform`
نوشته می‌شود که شامل پرووایدرهایی[^4]
است که در زیرساخت خود استفاده می‌کنید.
برای هر پرووایدر، صفت
`source`
مقادیر اختیاری
hostname
،namespace
و
provider type
را تعریف می‌کنید. ترافورم پرووایدرهای مورد نیاز را از
[Terraform Registry](https://registry.terraform.io/)
نصب می‌کند. در این مثال منبع پرووایدر
`aws`
به صورت
`hashicorp/aws`
تعریف شده که مخفف
`registry.terraform.io/hashicorp/aws`
است.

برای هیچ پرووایدری که در قطعه کد
`required_providers`
نوشته‌اید می‌توانید ورژن[^5]
آن را مقداردهی کنید. ورژن نیز یک متغیر اختیاری است، اما توصیه می شود که آن را تعریف کنید.
اگر مقداری برای آن نگذارید، ترافورم به صورت خودکار جدیدترین ورژن را هنگام شروع پروژه دریافت می‌کند.

برای یادگیری بیشتر به این 
[مستند](https://developer.hashicorp.com/terraform/language/providers/requirements) 
مراجعه کنید.

### provider
قطعه کد
`provider`
پرووایدرهایتان را نصب می‌کنید، در این مثال
`aws`
است.
پرووایدر یک
plugin
است که ترافورم از آن استفاده می‌کند تا منابع را مدیریت کند.

می‌توانید چند قطعه کد پرووایدر در فایل پیکربندی خود داشته باشید تا منابع خود را از
پرووایدرهای مختلف مدیریت کنید. حتی می‌توانید از پرووایدرهای مختلفی به صورت همزمان استفاده کنید.

### resources
این بخش مهم‌ترین بخش فایل پیکربندی است. در هر قطعه کد
`resource`
یک مولفه از زیرساخت خود را تعریف می‌کنید. یک ریسورس[^6]
می‌تواند یک مولفه فیزیکی یا مجازی مانند
EC2 instance،
یا می‌تواند یک منبع منطقی مانند
Heroku application
باشد.

هر قطعه کد ریسورس دو رشته قبل از شروع دارد: تایپ ریسورس و اسم ریسورس. در این مثال
تایپ ریسورس یک
`aws_instance`
و اسم آن
`app_server`
است. پیشوند یک تایپ نمایانگر پرووایدر مربوطه است. با تایپ و اسم ریسورس یک
ID
یکتا برای ریسورس ساخته می شود. در این مثال
ID
ریسورس
EC2 instance
شما
`aws_instance.app_server`
است.

در این قطعه کد تعدادی آرگومان وجود دارد که اطلاعات مربوط به ریسورس را می‌دهید.
آرگومان‌ها می‌تواند شامل چیزهایی مانند اندازه ماشین، اسم دیسک ایمج یا
VPC IDs
باشد. هر پرووایدر لیست آرگومان‌های اجباری و اختیاری را برای هر ریسورس در 
[مراجع](https://developer.hashicorp.com/terraform/language/providers)
خود نوشته است.

## مقداردهی اولیه پوشه
وقتی یک فایل پیکربندی جدید می‌سازید، در ابتدا باید پوشه را با
`terraform init`
مقداردهی اولیه کنید.
با این دستور
پرووایدرهای مختلف دانلود و نصب می‌شوند. در این مثال ما پرووایدر
`aws`
است.

```shell
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/aws versions matching "~> 4.16"...
- Installing hashicorp/aws v4.17.0...
- Installed hashicorp/aws v4.17.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

ترافورم پرووایدر
`aws`
را دانلود می‌کند و آن را در یک زیرپوشه مخفی به نام
`.terraform`
نصب می‌شود. دستور
`terraform init`
ورژن پرووایدری که نصب شده را چاپ می‌کند. همچنین یک فایل قفل به نام
`.terraform.lock.hcl`
می‌سازد که در آن ورژن هر پرووایدری که استفاده شده را می‌نویسد و هر وقت که بخواهید ورژن یک پرووایدر را آپدیت کنید، می‌توانید آن را تغییر دهید.

## فرمت و اعتبارسنجی پیکربندی
ما توصیه می‌کنیم که در تمام پرونده‌های پیکربندی خود از فرمت‌بندی یکنواخت استفاده کنید. دستور 
`terraform fmt`
به طور خودکار پیکربندی‌ها را در پوشه فعلی به منظور خوانایی و یکنواختی به‌روزرسانی می‌کند.

پیکربندی خود را فرمت کنید. 
Terraform 
در صورت وجود هرگونه تغییر در پرونده‌ها، نام فایل‌هایی که تغییر کرده‌اند را چاپ خواهد کرد.
در این مورد، پرونده پیکربندی شما به درستی فرمت‌بندی شده بود، بنابراین 
Terraform 
هیچ نام فایلی را برنخواهد گرداند.

```shell
$ terraform fmt
```

همچنین شما می‌توانید با استفاده از دستور 
`terraform validate`،
اطمینان حاصل کنید که پیکربندی شما در نحوه نوشتاری صحیح بوده و داخلیاً سازگار است.

پیکربندی خود را اعتبارسنجی کنید. پیکربندی مثال فوق معتبر است، بنابراین 
Terraform 
پیام موفقیت را برمی‌گرداند.

```shell
$ terraform validate
Success! The configuration is valid.
```

## ساخت زیرساخت
ساخت پیکربندی خود را با دستور
`terraform apply`
اعمال کنید.
Terraform
خروجی‌ای مشابه به پیام پایین خواهد داشت. مقداری از خروجی را حذف کردیم تا در فضا ذخیره‌سازی انجام داده باشیم.

```shell
$ terraform apply

Terraform used the selected providers to generate the following execution plan.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

   aws_instance.app_server will be created
  + resource "aws_instance" "app_server" {
      + ami                          = "ami-830c94e3"
      + arn                          = (known after apply)
#...

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
```

!!! Tip
    اگر پیکربندی شما قابل اجرا نیست، ممکن است منطقه خود را سفارشی کرده یا شبکه خصوصی پیش‌فرض خود را حذف کرده باشید. برای رفع مشکل به بخش رفع اشکال این آموزش مراجعه کنید.

قبل از اعمال هرگونه تغییری، Terraform برنامه اجرایی را چاپ می‌کند که عملیاتی که Terraform باید انجام دهد تا زیرساخت شما با پیکربندی هماهنگ شود را توصیف می‌کند.

فرمت خروجی مشابه فرمت diff تولید شده توسط ابزارهایی مانند Git است. در خروجی، + در کنار aws_instance.app_server وجود دارد که به معنای ایجاد این منبع توسط Terraform است. در زیر آن، ویژگی‌هایی که باید تنظیم شوند نمایش داده می‌شود. زمانی که مقداری که نمایش داده شده است (پس از اعمال)، به این معنی است که تا زمانی که منبع ایجاد شود، مقدار آن قابل شناسایی نخواهد بود. به عنوان مثال، AWS پس از ایجاد، نام‌های منابع منابع Amazon (ARN) را به نمونه‌ها اختصاص می‌دهد، بنابراین Terraform نمی‌تواند تا زمانی که تغییر را اعمال کنید و ارائه دهنده AWS مقدار مربوط به ARN را از API AWS برگرداند، مقدار ویژگی arn را بداند.

Terraform در حال حاضر متوقف شده و در انتظار تأیید شما برای ادامه عملیات است. اگر هر چیزی در برنامه اجرایی نادرست یا خطرناک به نظر می‌رسد، قبل از اینکه Terraform زیرساخت شما را تغییر دهد، ایمن است اینجا را متوقف کنید.

در این مورد، برنامه اجرایی قابل قبول است، بنابراین برای ادامه، در پرسش تأیید، بله را تایپ کنید. اجرای برنامه چند دقیقه طول می‌کشد زیرا Terraform منتظر می‌ماند تا نمونه EC2 در دسترس شود.

```shell
 Enter a value: yes

aws_instance.app_server: Creating...
aws_instance.app_server: Still creating... [10s elapsed]
aws_instance.app_server: Still creating... [20s elapsed]
aws_instance.app_server: Still creating... [30s elapsed]
aws_instance.app_server: Creation complete after 36s [id=i-01e03375ba238b384]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

زیرساخت شما با استفاده از
Terraform
ایجاد شده. از
[EC2 console](https://console.aws.amazon.com/ec2/v2/home?region=us-west-2#Instances:sort=instanceId)
بازدید کنید و ماشین خود را مشاهده کنید.

## بازرسی وضعیت
وقتی که پیکربندی خود را اعمال کردید،
Terraform
اطلاعات را در یک فایل به نام
`terraform.tfstate`
نوشته شده است.
Terraform
مشخصات ریسورس‌هایی که مدیریت می‌کند را در این فایل ذخیره می‌کند، تا بتواند در ادامه آپدیت و نابود کردن آن را انجام دهد.

این فایل تنها روشی است که
Terraform
می‌تواند ریسورس‌هایی که ساخته است را دنبال کند. بعضا شامل اطلاعات محرمانه‌ای است، پس باید آن را امن نگه دارید و فقط کسانی به آن دسترسی داشته باشند که لازم است.

وضعیت فعلی را با
`terraform show`
بازرسی کنید.

```shell
$ terraform show
# aws_instance.app_server:
resource "aws_instance" "app_server" {
    ami                          = "ami-830c94e3"
    arn                          = "arn:aws:ec2:us-west-2:561656980159:instance/i-01e03375ba238b384"
    associate_public_ip_address  = true
    availability_zone            = "us-west-2c"
    cpu_core_count               = 1
    cpu_threads_per_core         = 1
    disable_api_termination      = false
    ebs_optimized                = false
    get_password_data            = false
    hibernation                  = false
    id                           = "i-01e03375ba238b384"
    instance_state               = "running"
    instance_type                = "t2.micro"
    ipv6_address_count           = 0
    ipv6_addresses               = []
    monitoring                   = false
    primary_network_interface_id = "eni-068d850de6a4321b7"
    private_dns                  = "ip-172-31-0-139.us-west-2.compute.internal"
    private_ip                   = "172.31.0.139"
    public_dns                   = "ec2-18-237-201-188.us-west-2.compute.amazonaws.com"
    public_ip                    = "18.237.201.188"
    secondary_private_ips        = []
    security_groups              = [
        "default",
    ]
    source_dest_check            = true
    subnet_id                    = "subnet-31855d6c"
    tags                         = {
        "Name" = "ExampleAppServerInstance"
    }
    tenancy                      = "default"
    vpc_security_group_ids       = [
        "sg-0edc8a5a",
    ]

    credit_specification {
        cpu_credits = "standard"
    }

    enclave_options {
        enabled = false
    }

    metadata_options {
        http_endpoint               = "enabled"
        http_put_response_hop_limit = 1
        http_tokens                 = "optional"
    }

    root_block_device {
        delete_on_termination = true
        device_name           = "/dev/sda1"
        encrypted             = false
        iops                  = 0
        tags                  = {}
        throughput            = 0
        volume_id             = "vol-031d56cc45ea4a245"
        volume_size           = 8
        volume_type           = "standard"
    }
}
```

زمانی که Terraform این نمونه EC2 را ایجاد کرد، همچنین اطلاعات فراداده منبع را از ارائه دهنده AWS جمع آوری کرد و این اطلاعات را در پرونده وضعیت نوشت. در آموزش‌های بعدی، شما پیکربندی خود را تغییر خواهید داد تا به این مقادیر ارجاع دهید تا سایر منابع و مقدارهای خروجی را پیکربندی کنید.

[^1]: Instance
[^2]: Environment Variable
[^3]: Deploy
[^4]: Provider
[^5]: Version
[^6]: Resource
