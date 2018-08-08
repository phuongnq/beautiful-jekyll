---
title: "Tìm hiểu về EV SSL certificate"
tags: [vietnamese]
categories: [programming, javascript]
share-img: /img/ev_ssl_certificate.jpeg
---

Trong thời đại ngày càng có nhiều vụ việc hack liên quan đến bảo mật thông tin cá nhân, chúng ta ngày càng quan tâm xem một trang web liệu có đủ bảo mật hay không. Đặc biệt là việc bảo mật các thông tin nhạy cảm như thông tin cá nhân, số thẻ tín dụng hay thông tin về tiền bạc tài khoản online.

Một trong những thông tin để người dùng đánh giá một trang web đó là trang đó có sử dụng `https`, giao thức **HTTP có bảo mật** hay không. Về cơ bản trang nào không dùng `https` thì là trang không đáng tin cậy. Trong số các trang dùng `https`, tức là có `SSL certificate` thì có một dạng certificate cao cấp nhất, đem lại sự tin cậy cao nhất cho khách hàng đó là **EV SSL Certificate**.

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

# Định nghĩa

* Tên đầy đủ: `Extended Validation SSL Certificate`

* Theo như [Wikipedia](https://en.wikipedia.org/wiki/Extended_Validation_Certificate):

> An Extended Validation Certificate (EV) is a certificate used for HTTPS websites and software that proves the legal entity controlling the website or software package. Obtaining an EV certificate requires verification of the requesting entity's identity by a certificate authority (CA).

Bằng việc dùng **EV SSL Certificate**, khi truy cập bằng browser, trên thanh địa chỉ trình duyệt sẽ hiển thị tên công ty kèm với một hình khoá màu xanh, chứng nhận trang web được verified bảo mật. Điều này còn giúp chứng minh rằng trang web không phải là một trang giả được clone lại. Do vậy **EV SSL Certificate** có quyền lực tối cao trong các loại certificate mà mọi website cần bảo mật nên có.

Chúng ta thường thấy **EV SSL Certificate** được dùng cho những trang web của ngân hàng, lĩnh vực liên quan tiền tệ, fintech hay những trang bán hàng online uy tín. Ví dụ về việc dùng **EV SSL Certificate** trên trang bán hàng online *Rakuten Ichiba*:

![](/img/rakuten_top_ev_certificate.png)

PC address bar:

![](/img/rakuten_top_ssl_certificate_pc.png)

# Một số dạng EV Certificate

Có một số lựa chọn khi dùng **EV Certificate** như sau:

* **One domain** - chỉ bảo mật cho một domain, phù hợp cho website nhỏ, online shop

* **Multi domain** - bảo mật cho nhiều domain/sub domain. Phù hợp cho dịch vụ web phức tạp, có nhiều sub domain.

* **Code Signing** - bảo mật cho sản phẩm số, ví dụ như là software hay driver cho thiết bị.

# Những trang web như thế nào thì cần *EV SSL Certificate*?

Như ở trên đã trình bày, bất kỳ trang web nào mà cần mã hoá mạnh, độ tin cậy cao và phải đảm bảo chắc chắn về thông tin người dùng đều nên dùng **EV SSL Certificate**. Đặc biệt những đơn vị làm việc liên quan đến tiền tệ, giao dịch online, ngân hàng thì bắt buộc phải sử dụng để giảm thiểu rủi ro thành đối tượng của lừa đảo.

Mặc dù vậy, không có nghĩa là những website khác không cần dùng. Thực tế, ngày nay người dùng càng ngày càng thông minh, quan tâm đến vấn đề bảo mật. Cho nên bất kỳ website nào thu thập dữ liệu cá nhân đều nên dùng **EV SSL Certificate** để tối ưu độ tin cậy của mình.

# Lợi ích của việc dùng EV SSL Certificate

* **Tạo niềm tin cho người dùng** - các browser hiện đại đều thiết kế để trang web có **EV SSL Certificate** hiển thị đẹp, với tên công ty và biểu tượng khoá an toàn màu xanh lá cây. Chỉ với việc nhìn thấy thanh địa chỉ như vậy cũng tạo cảm giác an tâm cho người dùng.

* **Tăng conversion rate** - như một hệ quả của việc trang web đáng tin, người dùng sẽ tự tin để click các bước tiếp theo, chẳng hạn để nhập số thẻ tín dụng mua hàng

* **Tăng độ trung thành của khách hàng** - Với hai lợi ích trên, khách hàng sẽ quay lại website thường xuyên hơn, xây dựng sự trung thành với trang web.

# Tại sao EV SSL Certificate có giá đắt?

Một đặc điểm của **EV SSL Certificate** là nó đắt hơn so với một certificate bình thường.

![](/img/sample_ev_ssl_price.png)

Tại sao lại như vậy?

Lý do là vì với một **EV SSL Certificate**, bên CA (certificate authority) sẽ phải làm một số bước chuyên biệt để đánh giá độ tin cậy của công ty đặt mua, việc này tốn về mặt thời gian và nhân sự. Do vậy, cho đến khi các công ty CA có giải pháp tối ưu bài toán thì một certificate EV sẽ vẫn có giá đắt hơn bình thường.

# Kết luận

> EV SSL Certificate là cần thiết cho các website mà có dùng thông tin cá nhân, login, thanh toán

Nó là một cách để nâng độ tin cậy của trang web trong mắt người dùng, đồng thời tăng conversion rate, độ trung thành của người dùng cho các dịch vụ online như là e-commerce.

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