---
title: "Performance Test với jMeter - Thread Group"
tags: [tech, performance test, stress test, vietnamese, jmeter]
share-img: /img/performance_test.png
---

**Các bài viết về Performance Test**

* [Các khái niệm liên quan Performance Test](https://phuongnq.me/2018-01-11-performance-test-with-jmeter-chapter01/)
* [jMeter là gì](https://phuongnq.me/2018-01-12-performance-test-with-jmeter-02/)
* [Cài đặt jMeter](https://phuongnq.me/2018-01-13-performance-test-with-jmeter-03/)
* [Test Plan trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-04/)
* [Thread Group trong jMeter](https://phuongnq.me/2018-01-14-performance-test-with-jmeter-05/)

## Thread Group

Một *Thread Group* trong jMeter biểu diễn cho một vùng chứa *virtual user* thực hiện nhóm các hoạt động nhất định. Để ví dụ, hãy tưởng tượng trường hợp tìm kiếm với Google, một nhóm người dùng có thể tìm kiếm với text, một nhóm khác thì tìm tin tức trên *Google News*, một nhóm nhỏ nữa thì tìm kiếm ảnh qua *image search*. Khi tạo script cho *performance test*, chúng ta sẽ tạo những nhóm *Thread Group* khác nhau, với số lượng khác nhau tùy theo từng screenario thực tế. Với mỗi nhóm *Thread User* như vậy, chúng ta sẽ thêm vào những thành phần con, ví dụ như *sampler* của *HTTP* khác nhau với từng nhóm, thể hiện request khác nhau tới server.

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

> Để tạo một Thread Group với jMeter:

Click chuột phải vào *Test Plan* -> **Add** -> **Threads (Users**) -> Click **Thread Group**

![Thread Group](/img/jmeter_thread_group.jpg)

## Các thuộc tính cho Thread Group

Như các thành phần khác, **Thread Group** có control panel (pane bên phải) để thiết lập các tham số trong *performance test* như là - số *virtual user* tạo ra, lập lịch cho test, thêm delay cho test,...

![Thread Group Properties](/img/jmeter_thread_group_property.jpg)

Hãy cùng nhau tìm hiểu các thuộc tính của *Thread Group*:

* **Name**

    Tên cho *Thread Group*, giá trị mặc định chính là *Thread Group*. Chúng ta có thể đổi tên này theo như ý thích, tùy vào mục đích sử dụng group đó. Ví dụ, cho việc đăng nhập thì có thể lấy tên là *LoginUsers*.

* **Comments**

    Đây là một tùy chọn không bắt buộc, mục đích chỉ là đưa ra thêm thông tin cho *Thread Group*. Thông tin này nên biểu diễn hoạt động của nhóm *virtual user* trong *Thread Group* hoặc thông tin metadata khác.

Tùy chọn trong mục `Action to be taken after a Sampler Error` dùng để thiết lập hành động khi có lỗi từ việc thực hiện `Sampler`. Lỗi này có thể do server không trả về đúng, hoặc lỗi do `assertion`.

* **Continue** - Giá trị mặc định, tiếp tục chạy test nếu có lỗi.

* **Start Next Thread Loop** - Tiếp tục với lượt chạy tiếp theo của thread.

* **Stop Thread** - Dừng thread hiện tại nếu có lỗi.


* **Stop Test** - Dừng hoạt động của thread một cách mượt mà, kết thúc *sampler request* hiện tại.

* **Stop Test Now** - Bắt buộc dừng ngay hoạt động của thread nếu có lỗi.

### Các thiết lập bên trong "Thread Properties"

* **Number of Threads(users)** - Số lượng *virtual user*.

* **Ramp-up Period(in seconds)** - Tổng thời gian (giây) để cho tất cả các thread bắt đầu chạy. Ví dụ - Nếu chúng ta muốn mỗi thread active trong 0.5s và có tổng cộng 20 threads thì *Ramp Up Time* sẽ là `20 * 0.5 = 10s`. Chúng ta sẽ tìm hiểu lợi ích cho việc dùng *Ramp-Up* trong những bài viết kế tiếp.

* **Loop Count** - Số lần lặp lại cho *thread group*. Giá trị mặc định là 1 nghĩa là không lặp lại.

* **Loop Count Forever** - Nếu tích chọn, giá trị *Loop Count* sẽ bị disable, lặp vô hạn cho đến đến khi dừng bằng tay.

* **Delay Thread Creation until needed** - Làm chậm việc tạo ra thread mới. Hữu ích khi tạo *Thread Group* với lượng *virtual user* lớn. Khi đó tránh được tải lớn do tạo ra một lượng user lớn ngay lập tức.

* **Scheduler** - Khi được tích, tùy chọn cho *schedulers* sẽ được enable để thiết lập việc chạy/dừng test tại những thời điểm nhất định. Nếu không chọn, bản test sẽ chạy ngay khi chúng ta bấm *Start*.

Giải thích cụ thể thiết lập bên trong "Scheduler Configuration":

* **Duration(seconds)** - Khoảng thời gian test, khi đạt đến mức này, test sẽ dừng lại.

* **Startup delay(seconds)** - Khi chạy *Test Script*, jMeter sẽ đợi cho đến khi đạt đến giá trị này (giây).

* **Start Time** - Trường này dùng để chỉ định thời điểm bắt đầu test. Chỉ có tác dụng khi trường *Duration* ở trên không được chọn.

* **End Time** - Trường này dùng để chỉ định thời điểm kết thúc test.  Chỉ có tác dụng khi trường *Duration* ở trên không được chọn.

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