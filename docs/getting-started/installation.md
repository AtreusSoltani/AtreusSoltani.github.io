# نصب کنید

## نصب و راه‌اندازی
=== "MacOS"
    با استفاده از
    Homebrew
    می‌توانید ترافورم را نصب کنید.

    در ابتدا باید
    HashiCorp tap
    را نصب کنید که تمامی پکیج‌های[^2]
    HashiCorp
    در آن است را نصب کنید.
    ```bash
    brew tap hashicorp/tap
    ```

    سپس ترافورم را با دستور زیر نصب کنید.
    ```bash
    brew install hashicorp/tap/terraform
    ```

    !!! توجه
        این دستور یک فایل باینری امضا شده را نصب می‌کند و با هر ریلیز[^3]
        رسمی نسخه به صورت خودکار آپدیت می‌شود.

=== "Ubuntu"
    مطمئن شوید که پکیج‌های
    `gnupg`،
    `software-properties-common`
    و
    `curl`
    را نصب کرده‌اید. به این پکیج‌ها برای نصب ترافورم احتیاج دارید.
    ```bash
    sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
    ```

    سپس باید
    HashiCorp GPG Key
    را نصب کنید.

    ```bash
    wget -O- https://apt.releases.hashicorp.com/gpg | \
    gpg --dearmor | \
    sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
    ```

    اثرانگشت کلید را تایید کنید.

    ```bash
    gpg --no-default-keyring \
    --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
    --fingerprint
    ```

    دستور
    `gpg`
    چنین خروجی‌ای می‌دهد.

    ```bash
    /usr/share/keyrings/hashicorp-archive-keyring.gpg
    -------------------------------------------------
    pub   rsa4096 XXXX-XX-XX [SC]
    AAAA AAAA AAAA AAAA
    uid           [ unknown] HashiCorp Security (HashiCorp Package Signing) <security+packaging@hashicorp.com>
    sub   rsa4096 XXXX-XX-XX [E]
    ```

    ریپازیتوری رسمی
    HashiCorp
    را به سامانه خود اضافه کنید.  با دستور
    `lsb_release -cs`
    توزیع مناسب برای لپتاپ خود را پیدا کنید و آن را نسب کنید.

    ```bash
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
    https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
    sudo tee /etc/apt/sources.list.d/hashicorp.list
    ```

    اطلاعات پکیج را دریافت کنید.

    ```bash
    sudo apt update
    ```

    ترافورم را نصب کنید.

    ```bash
    sudo apt-get install terraform
    ```

## تایید نصب
نصب شدن ترافورم را با باز کردن یک ترمینال[^4]
جدید و لیست کردن دستورات موجود ترافورم تایید کنید.

```shell
$ terraform -help
Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.
##...
```

[^1]: Command Line Interface
[^2]: Package
[^3]: Release
[^4]: Terminal