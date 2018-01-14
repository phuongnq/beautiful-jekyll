---
title: "Performance Test với jMeter - Cài đặt"
tags: [tech, performance test, stress test, vietnamese, jmeter]
share-img: /img/performance_test.png
---

**Các bài viết về Performance Test**

* [Các khái niệm liên quan Performance Test](https://phuongnq.me/2018-01-11-performance-test-with-jmeter-chapter01/)
* [jMeter là gì](https://phuongnq.me/2018-01-12-performance-test-with-jmeter-02/)
* [Cài đặt jMeter](https://phuongnq.me/2018-01-13-performance-test-with-jmeter-03/)
* [Test Plan trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-04/)

Trong bài viết này, chúng ta sẽ cùng tìm hiểu cách cài đặt **jMeter** trên Windows, Linux và MacOS. Vì *jMeter* là ứng dụng chạy trên nền *Java*, cần chắc chắn rằng hệ điều hành của bạn đã cài bản mới nhất cho **máy ảo Java (JVM)**.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

## Cài đặt trên Windows

* Tải bản binary trên [trang chủ jMeter](http://jmeter.apache.org/download_jmeter.cgi). Tại thời điểm viết bài, bản mới nhất là *apache-jmeter-3.3.zip*.

* unzip file nén tải ở bước trên vào thư mục muốn cái đặt *jMeter*.

* Chạy file cài đặt bằng việc double click vào file `jmeter.bat` trong thư mục `bin`.

Nếu không có vấn đề gì về môi trường *Java*, GUI của *jMeter* sẽ xuất hiện sẵn sàng để sử dụng.

## Cài đặt trên Linux

> Do *jMeter* có file chạy trên máy ảo *Java* nên chúng ta có thể cài đặt giống như với bản cho Windows.

* Tải bản binary *apache-jmeter-3.3.tgz* trên trang chủ.

* Giải nén ra thư mục muốn cài đặt. Thông thường có thể dùng thư mục `~/opt/apache-jmeter`.

* Chạy file `jmeter.sh` trong thư mục `bin` để dùng GUI.

> Ngoài ra xin hướng dẫn thêm một cách cài đặt dùng dòng lệnh

```
sudo apt-get install jmeter
```

Sau khi cài đặt thành công, kiểm tra thư mục cài đặt:

```
$ which jmeter
/usr/bin/jmeter
```

Chạy *jMeter* với GUI:

```
$ jmeter
Jan 13, 2018 2:53:44 PM java.util.prefs.FileSystemPreferences$1 run
INFO: Created user preferences directory.
....
```

![jMeter GUI](/img/jmeter.png)

## Cài đặt trên MacOS

> Cũng giống như với **Linux**, chúng ta có thể tải bản binary từ trang chủ và cài đặt vào thư mục `~/opt/apache-jmeter`.

Một mẹo nhỏ để mở từ dòng lệnh:

Thêm vào file `~/.bash_profile` dòng sau:

```
alias jmeter='open ~/opt/apache-jmeter/bin/ApacheJMeter.jar'
```

Mở terminal mới, chúng ta có thể dùng lệnh `jmeter` từ console để khởi động GUI.

> Một cách cài đặt khác cho người dùng **Homebrew**

Để cài đặt jMeter gõ lệnh

```
brew install jmeter
```

Sau khi cài đặt thành công, kiểm tra thư mục cài đặt:

```
$ which jmeter
/usr/local/bin/jmeter
```
Chạy *jMeter* với GUI:

```
$ jmeter
================================================================================
Don’t use GUI mode for load testing, only for Test creation and Test debugging !
For load testing, use NON GUI Mode:
  jmeter -n -t [jmx file] -l [results file] -e -o [Path to output folder]
& adapt Java Heap to your test requirements:
  Modify HEAP=“-Xms512m -Xmx512m” in the JMeter batch file
================================================================================
....
```
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

