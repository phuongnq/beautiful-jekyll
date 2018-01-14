---
title: "Performance Test với jMeter - Test Plan"
tags: [tech, performance test, stress test, vietnamese, jmeter]
share-img: /img/performance_test.png
---

**Các bài viết về Performance Test**

* [Các khái niệm liên quan Performance Test](https://phuongnq.me/2018-01-11-performance-test-with-jmeter-chapter01/)
* [jMeter là gì](https://phuongnq.me/2018-01-12-performance-test-with-jmeter-02/)
* [Cài đặt jMeter](https://phuongnq.me/2018-01-13-performance-test-with-jmeter-03/)
* [Test Plan trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-04/)
* [Thread Group trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-05/)

## Thế nào là Test Plan

*Test Plan* là một thành phần container logic chứa những lệnh khác nhau cần thiết cho việc *performance test*. Những hoạt động khác nhau này được thực hiện bởi những thành phần khác nhau trong *Test Plan*. *jMeter* có cung cấp giao diện GUI cho việc thêm, xóa, và thiết lập các thành phần của *Test Plan*.

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

> Ví dụ về các thành phần của một Test Plan

![Test Plan Element](/img/jmeter_test_plan.png)

Như trong screenshot ở trên chúng ta có thể thấy hai vùng cửa sổ. Phần bên trái hiển thị các thành phần của một *Test Plan*. Chúng ta có thể thêm, bớt các thành phần này. Phần bên phải hiển thị cụ thể các thiết lập cho một thành phần của *Test Plan* hoặc thiết lập cho chính *Test Plan* đó.

## Những thành phần thường được dùng trong Test Plan

* **Thread Group**

    Dùng để biểu diễn **virtual user** trong *performance test*, có nghĩa là người dùng sẽ truy cập vào trang web. Trong một *Test Plan*, đơn giản nhất thì chúng ta chỉ cần một *Thread Group*. Tuy nhiên, để phục vụ cho nhiều sceenario khác nhau, chúng ta có thể tạo ra nhiều *Thread Group* khác nhau.

* **Sampler**

    *Sampler* là các loại *request* khác nhau gửi đến server phục vụ cho việc test. *JMeter* cung cấp nhiều loại *sampler* khác nhau như là *HTTP*, *FTP*, *TCP*, *JDBC*.

* **Logic Controller**

    Bằng việc sử dụng *Logic Controller*, chúng ta có thể tùy biến cách mà *Sampler* gửi request đến server. Một ví dụ cơ bản cho cách dùng *Logic Controller* là việc dùng *Loop Controller* (vòng lặp) để gửi request nhiều lần tới server.

* **Timers**

    *Timers* dùng để tạm dừng hoạt động test cho một khoảng thời gian định trước. Về cơ bản, chúng ta dùng *Timers* để biểu diễn thời gian đợi của người dùng thực tế (wait time) hoặc thời gian suy nghĩ (think time).

* **Assertions**

    **Assertions** như tên gọi của nó, dùng để xác nhận kiểm tra xem response của server có đúng hay không.

* **Listeners**

    Listeners in JMeter are used to save, view and analyze the test results in graphical or tabular forms.

    **Listeners** dùng để lưu, hiển thị và đánh giá kết quả test. Có nhiều cách hiển thị khác nhau, như là dùng đồ thị, text, hoặc bảng biểu.

Trên đây nêu ra một số thành phần cơ bản cho *Test Plan*. Tuy nhiên, thực tế có nhiều thành phần hơn nữa, như là thành phần để đọc file CSV, thành phần để tạo biến,... Tham khảo thêm: [jMeter Manual](http://jmeter.apache.org/usermanual/index.html).

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