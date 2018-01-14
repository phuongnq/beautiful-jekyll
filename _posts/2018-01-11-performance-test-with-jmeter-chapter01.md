---
title: "Performance Test với jMeter - Các khái niệm chung"
tags: [tech, performance test, stress test, vietnamese, jmeter]
share-img: /img/performance_test.png
---

**Các bài viết về Performance Test**

* [Các khái niệm liên quan Performance Test](https://phuongnq.me/2018-01-11-performance-test-with-jmeter-chapter01/)
* [jMeter là gì](https://phuongnq.me/2018-01-12-performance-test-with-jmeter-02/)
* [Cài đặt jMeter](https://phuongnq.me/2018-01-13-performance-test-with-jmeter-03/)
* [Test Plan trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-04/)

# Các khái niệm liên quan tới Performance Test

Hầu hết mục đích của các dịch vụ web là muốn có một lượng user đủ lớn, và thực tế là các trang web luôn cố gắng để tăng lượng user base này. Những ứng dụng web như vậy cần đảm bảo cung cấp dịch vụ sao cho có thể chạy ổn định khi mà user tăng lên, hay nói cách khác cần đảm bảo có thể scale được. Trong trường hợp đó, việc kiểm tra performance của trang web là rất cần thiết, để chắc chắn được một ứng dụng web tốt đến mức nào khi lượng user tăng đột biến trong những tình huống nhất định.

Trong nhiều trang liên quan đến bán hàng online, gaming hay social networking thì có thể chúng có một vài tính năng chung, nhưng điểm nổi bật giúp ta phân biệt các trang web chính là performance của trang web đó. Performance là yếu tố sống còn của trang web khi scale, và để biết trước điều này, chúng ta dùng **Performance Test**.

![Performance Test](/img/performance_test.png)

## Tại sao chúng ta cần Performance Test?

Có nhiều lý do để thực hiện *Performance Test*, sau đây là một số lý do critical:

* **Cung cấp một thước đo cho tốc độ của hệ thống**: Việc test giúp chúng ta benchmark các thông số như *response time*, cũng chính là thước đo tốc độ của ứng dụng. Điều này cực kỳ quan trọng khi đánh giá sự thành công của một trang web.

* **Giúp đánh giá khả năng scale của ứng dụng**: Performance giúp đánh giá xem liệu trang web có thể scale tới mức nào, khi lượng user tăng lên.

* **Giúp kiểm tra độ chắc chắn của ứng dụng**: Stress test giúp chúng ta kiểm tra xem web hoạt động như thế nào khi mà lượng workload lớn hơn mức dự kiến. Điều này giúp biết được web sẽ gặp bao nhiêu lỗi, lỗi như thế nào khi load quá tải.

* **Giúp đánh giá độ tin cậy của ứng dụng**: Nhiều kiểu *performance test* khác nhau giúp đánh giá độ tin cậy và cho biết độ chính xác cũng như tính nhất quán của output. 

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

## Phân biệt Performance Test với Load Test

*Load Test* thực ra là một nhánh của *performance test*, tập trung vào việc phân tích hoạt động của web trong một độ tải nhất định trong một khoảng thời gian được định trước. Trong khi đó, *performance test* hiểu rộng hơn là việc kiểm tra nhiều khía cạnh của hệ thống như là trạng thái hoạt động của web khi tải lớn hơn mức ổn định (**stress test**); performance của ứng dụng với một lượng dữ liệu lớn (**volume test**); khả năng chịu đựng của ứng dụng ở mức tải bình thường nhưng trong một khoảng thời gian dài (**endurance**),...

## Phân loại Performance Test

Như đề cập ở phần trên, *Performance Test* hiểu rộng là việc test để đánh giá một cách toàn diện về ứng dụng web. Và để tiện cho việc đánh giá từng khía cạnh riêng, nó được chia ra thành vài loại:

* **Load Test**

  *Load Test* là một dạng kiểm thử đánh giá performance của hệ thống trên lượng tải đã được ước lượng trước. Các thông số thường cần đánh giá như là: *response time*, *throughput*, *error rate*, ...

  Ví dụ về *Load Test*:

  > Một vài lập trình viên code ứng dụng web có khả năng chịu tải khoảng 1000 concurrent user. Trong trường hợp này họ sẽ tạo *load test* với 1000 *virtual user*, chạy trong duration khoảng 1-2h. Sau khi chạy thì họ có thể phân tích kết quả, đánh giá xem hoạt động của trang web như thế nào.

* **Stress Test**

  *Stress Test* là một dạng kiểm nghiệm đánh giá hệ thống tại mức tải lớn hơn mức tải ước lượng trước. Một điểm nữa của *stress test* là để đánh giá điểm **break point** của ứng dụng, xem tại điểm nào thì sẽ bắt đầu response không đúng.

  Ví dụ về *Stress Test*:
  > Ứng dụng ở trên thiết kế mức tải với 1000 user, nhưng chúng ta chạy với 1400 user và kiểm tra xem ứng dụng có bị crash không.

* **Endurance Test**

  Còn được biết đến với tên gọi là *Soak Test*. *Enduration Test* đánh giá độ ổn định của hệ thống cho một thời gian test dài. Những vấn đề như là *memory leak* có thể phát hiện trong quá trình test.

  Ví dụ về *Enduration Test*:
  > Ứng dụng bán hàng online cần chịu tải liên tiếp cho nhiều user khác nhau, mua hàng khác nhau. Trong những ứng dụng kiểu này vấn đề *memory leak* rất quan trọng. Chúng ta có thể thử test từ 1 ngày đến 2 ngày liên tục để kiểm tra độ dùng *memory*.

* **Spike Test**

  Với *spike test*, chúng ta phân tích hoạt động của hệ thống khi đột ngột lượng user tăng lên đáng kể. Nó cũng gồm cả việc kiểm tra xem ứng dụng có phục hồi được sau khi lượng user giảm lại mức bình thường.

  Ví dụ về *Spike Test*:
  > Một trang bán hàng online thực hiện quảng cáo dịp sale, lượng user tăng đột biến trong một lượng thời gian ngắn. *Spike test* dùng để phân tích trong tình huống này.

* **Volume Test**

  *Volume Test* được thực hiện bằng cách dùng ứng dụng với một lượng dự liệu lớn. Ví dụ có thể `insert` nhiều dữ liệu vào database hoặc cho ứng dụng xử lý file dung lượng lớn. Bằng việc làm *volume Test* chúng ta biết được điểm *bottleneck* của ứng dụng khi lượng dữ liệu tăng cao.

  Ví dụ về *Volume Test*:
  > Với một ứng dụng bán hàng online vừa mới được release, chúng ta insert hàng triệu dòng vào database và đánh giá performance.

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