---
layout: post
title: "Giới thiệu về Django"
subtitle: "Giới thiệu về Django"
date: 2020-06-08 16:50:00 +0700
background: '/img/posts/01.jpg'
permalink: /django-gioi-thieu/
---

<h2 class="section-heading">Django – Giới thiệu</h2>

<p><i>Django</i> là một web framework miễn phí mã nguồn mở được viết bằng Python. Django sử dụng mô hình Model-View-Control (MVC). Django được phát triển bởi <i>Django Software Foundation(DSF)</i> – một tổ chức phi lợi nhuận độc lập.</p>

<p>Mục tiêu chính của Django là đơn giản hóa việc tạo các website phức tạp có sử dụng cơ sở dữ liệu. Django tập trung vào tính năng “có thể tái sử dụng” và “có thể tự chạy” của các component, tính năng phát triển nhanh, không làm lại những gì đã làm. Một số website phổ biến được xây dựng từ Django là Pinterest, Instagram, Mozilla, và Bitbucket.</p>

<h2 class="section-heading">Cài đặt Django</h2>

<p>Để có thể sử dụng Django thì bạn nhất định phải cài Python trong máy mình rồi, và khi cài thì Python có kèm theo một chương trình có tên là pip, đây là một phần mềm quản lý các gói mở rộng dành cho Python. Để cài đặt Django thì bạn sẽ dùng đến pip.</p>

<p>Bạn mở Command Prompt (cmd) lên và gõ lệnh:</p>

```
pip install Django
```

<p>Để Python cài đặt gói Django mới nhất, gói này sẽ nằm trong thư mục Lib/site-packages trong thư mục cài đặt Python, hoặc gõ lệnh:</p>

```
pip install Django==1.9.4
```

<p>để cài đặt gói Django phiên bản 1.9.4, đây là phiên bản mà mình sử dụng để viết series này.</p>

<p>Nếu khi cài Python bạn không cài pip thì bạn có thể lên trên trang GitHub của Django để tải về tại địa chỉ <a href="https://github.com/django/django.git">django</a></p>

<h2 class="section-heading">Xem phiên bản Django</h2>

<p>Sau khi cài đặt xong gói Django, bạn có thể kiểm tra một số thông tin của gói này.</p>

```
## version.py

import django
print(django.get_version())
```

<p>Bằng cách dùng phương thức django.get_version().</p>


```
## Output

1.9.4
```

