---
title: "Performance Test với jMeter - Giới thiệu"
tags: [tech, performance test, stress test, vietnamese, jmeter]
share-img: /img/performance_test.png
---

**Các bài viết về Performance Test**

* [Các khái niệm liên quan Performance Test](https://phuongnq.me/2018-01-11-performance-test-with-jmeter-chapter01/)
* [jMeter là gì](https://phuongnq.me/2018-01-12-performance-test-with-jmeter-02/)
* [Cài đặt jMeter](https://phuongnq.me/2018-01-13-performance-test-with-jmeter-03/)
* [Test Plan trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-04/)
* [Thread Group trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-05/)

## JMeter là gì?

**JMeter** là một ứng dụng desktop viết bằng *Java* dùng cho *performance test* nhiều loại ứng dụng client-server như là website, web service, database, FTP server,... jMeter thuộc dạng ứng dụng open source cung cấp bởi *Apache* và không hề mất phí cho quyền sử dụng. Tham khảo thêm thông tin trên [trang chủ](http://jmeter.apache.org/)

![jmeter logo](/img/jmeter_logo.svg)

Các dạng ứng dụng có thể test được với *jMeter*:

* Websites - HTTP và HTTPS

* Web Services - REST và SOAP

* Database Servers

* FTP Servers

* LDAP Servers

* Mail Servers - SMTP, POP3, IMAP

* Shell Scripts

* TCP Servers

## Lợi ích của việc dùng *jMeter*

1. Hoàn toàn miễn phí - do là open source và không có một khoản phí license nào.

2. Khả năng dùng rộng rãi - có thể dùng cho *performance test* của các ứng dụng như là - Web applications, web services, database, LDAP, shell scripts,...

3. Độc lập về môi trường - jMeter được viết hoàn toàn bằng Java, do vậy có thể chạy trên Windows, MacOS hay Unix/Linux.

4. Có tính năng Record & Playback - jMeter cung cấp tính năng record & playback cùng với giao diện drop & drag giúp việc tạo script dễ dàng hơn.

5. Khả năng tuỳ biến - Do là open source nên có thể tuỳ biến nếu người dùng muốn. Ví dụ so với các dịch vụ cloud, jMeter có thể tuỳ biến dễ dàng để là việc với proxy.

6. Đối ứng việc test phân tán - jMeter có thể tạo thiết lập master/slave để tiến hành test trên nhiều máy.

7. Community lớn - trên mạng có sẵn nhiều tutorial cũng như community trợ giúp. Ngoài ra nó cũng cung cấp nhiều plugin bổ trợ cho việc tạo script và phân tích.

## Hạn chế của *jMeter*

1. Việc viết script cho jMeter ban đầu mất thời gian học và hiểu các khái niệm như regular expressions, session handling hay các element của jMeter.

2. Không có tính năng thể hiện network visualisation.

3. Một máy đơn lẻ có thể không phù hợp cho việc tiến hành test với lượng virtual user lớn. Trong trường hợp này, có thể cần đưa máy lên cloud, thực hiện test phân tán.

4. Không hỗ trợ tốt ajax, JavaScript hay render element của trang web.

5. Cung cấp không nhiều biểu diễn real time.

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