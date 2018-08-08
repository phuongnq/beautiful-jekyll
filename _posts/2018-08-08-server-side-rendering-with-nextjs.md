---
title: "Implement dịch vụ web server side rendering với NextJS"
tags: [programming, web]
categories: [programming]
share-img: /img/nextjs.png
---

Cho đến hiện tại, kiến trúc phổ biến cho **web service** vẫn là **client/server**. Kiến trúc này giúp chúng ta có nhiều *client* có thể kết nối đến cùng một *backend* chung; như là: ứng dụng mobile, các node client IoT, REST API...

Trong quá khứ, *backend* thường là node chịu rất nhiều tải, và nó cố gắng làm mọi thứ: từ việc kết nối CSDL, render HTML, lưu trữ *static assets* (ảnh, css, js...) và thường được biết đến như là kiến trúc **monolithic**.

Ngày nay, chúng ta đều biết rằng kiến trúc tập trung vào một *backend* như vậy không hiệu quả, khó scale. Kiến trúc web hiện tại phân chia rõ ràng công việc giữa *server* và *client*:

* Server có nhiệm vụ làm việc với dữ liệu

* Client có nhiệm vụ hiển thị dữ liệu đó (presentation)

![](/img/nextjs.png)

# Thế nào là single-page app

Hiểu đơn giản thì một trang web là single-page app khi mà nó tải về JavaScript từ server, chạy toàn bộ phần render hiển thị phía browser. Dữ liệu sẽ được lấy từ server để hiển thị thông qua **API call**.

Chúng ta gọi là single-page app là vì server không trực tiếp render toàn bộ trang HTML cho client. Server chỉ có nhiệm vụ trả về phần HTML đơn giản nhất + JavaScript code cho client. Tất cả các vấn đề còn lại như là: page rendering, navigate giữa các routes sẽ được thực hiện từ phía client, bằng JavaScript.

Dễ nhận thấy lợi ích của single-page app là chúng ta không cần phải download lại trang mỗi lần chuyển qua chuyển lại giữa các page.

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

# Giới thiệu về React

ReactJS là một bộ thư viện JavaScript đang rất được ưa thích và đặc biệt phù hợp cho việc tạo single-page app.

Trang chủ: [https://reactjs.org/](https://reactjs.org/)

Đặc điểm nổi bật của **ReactJS** là nó dùng virtual DOM, source code cho HTML mixing với JavaScript trong cùng một file duy nhất.

Một đơn vị nhỏ nhất của React là một **Component**. Một page HTML sẽ do nhiều **Component** cấu tạo nên. Có rất nhiều open source component trên mạng để chúng ta dùng lại. Ví dụ như component để tạo calendar, pagination, form...

# Vấn đề performance của single-page app

Như được trình bày ở trên, với **single-page app** thì chúng ta cần phải download về tất cả asset cho trang web trước khi sử dụng: JavaScript files, CSS files, và có thể cả các files ảnh nữa. Trong phần lớn trường hợp chúng ta sẽ phải module hoá files dẫn đến một app scale sẽ có rất rất nhiều file JavaScript nhỏ.

Với kiến trúc **single-page app**, chúng ta sẽ phải dùng API khá nhiều. Với mỗi dữ liệu cần hiển thị, sẽ cần một API request tương ứng tới một backend nào đó.

Tổng hợp của 2 điều trên, mỗi **single-page app** đều có một vấn đề performance chung: đó là thời gian load lần đầu (*initial load time*) rất lớn. Chúng ta đều biết, trung bình sau 2-3 giây mà trang web chưa được load thì người dùng sẽ bỏ cuộc, không quay lại trang web nữa.

Một vấn đề nữa là về **search engine optimization (SEO)**. Engine tìm kiếm của Google đánh giá cao trang web có load time nhỏ.

Để giải quyết vấn đề này thì chúng ta có thể dùng kỹ thuật **server-side rendering**.

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

# server-side rendering với React

Hiểu đơn giản thì **server-side rendering** có bước render đầu ở phía server, các page khác khi browsing (click button, link) sẽ được render từ phía client.

**server-side rendering** sinh ra để giải quyết vấn đề **initial load time** cho ứng dụng **single-page app**. Như chúng ta đều biết, render từ server rồi gửi về client thì sẽ nhanh hơn là render hoàn toàn ở client. Lý do là bên server có thể cache các component để dùng lại khi có một request mới gửi đến, ngoài ra thời gian **API call** từ phía server cũng ngắn hơn so với từ client.

Để implement **server-side rendering** thì chúng ta cần dùng chung kỹ thuật cả phía server lẫn client (dễ nghĩ ngay đến việc dùng JavaScript). Một ứng dụng có template cả phía server và client, dùng chung một kỹ thuật cả 2 phía được gọi là **universal app** hoặc **isomorphic app**.

Hướng implement sẽ thường như sau:

* Dùng NodeJS server, install web framework và listen incoming request.

* Với mỗi request tương ứng một URL nào đó, ta lấy script tương ứng, bootstrap trạng thái đầu cho page đó. Rồi render HTML cùng với data gửi về client page tương ứng URL được gọi.

* Client nhận được HTML, nhanh chóng hiển thị với data và state có được từ server. Đồng thời kiểm soát các hoạt động browsing tiếp theo.

* Khi người dùng click (button, link) tiếp theo, trang mới sẽ được render hoàn toàn từ phía client. Chỉ có phần **API call** là được gọi **HTTP request** đến remote server nào đó.

Theo như hướng implement trên thì không phải bất kỳ web framework nào cũng làm được việc đó. Ví dụ nếu muốn implement với **jQuery** là rất khó.

Rất may là 2 đặc tính quan trọng của ReactJS (implement theo hướng dùng state và có thể render HTML) thì thư viện này là một lựa chọn hoàn hảo cho **server-side rendering**.

**server-side rendering** cũng được chia thành một số nhóm:

* Drop-in dynamic solutions (Next.js, Electrode, After)

* Drop-in static solutions (Gatsby, React Static)

* Custom solutions

**Static solution**, như chúng ta biết một số thư viện nổi tiếng như là **Gatsby**, build React Component thành các files HTML và các file này được host trên static server (như Nginx, Apache) và hiểu như là static website. (Bản thân trang blog https://phuongnq.me cũng là một trang static).

**Dynamic solution**, thì hơi khác, chúng render HTML mỗi khi có request từ client gửi đến. Điều này có nghĩa chúng ta có thể làm mọi việc tương tự như một dynamic web service truyền thống, với logic và dữ liệu phức tạp.

**NextJS** là một trong những **dynamic solution** cho **server-side rendering**. Hiện đang là một lựa chọn khá tốt và nổi bật trong số web framework. Với **NextJS** chúng ta có thể dễ dàng xây dựng bộ khung cho web service nhanh chóng, với ít configuration.

Xem thêm một số bài viết về **NextJS** tại đây:

- [Create a website scraper with NextJS](https://phuongnq.me/2018-01-27-web-scraper-with-nextjs/)

- [Use Nprogress module with NextJS](https://phuongnq.me/2018-02-02-use-nprogress-with-nextjs/)

- [Boilerplate for NextJS with Material Design included](https://phuongnq.me/2018-03-09-nextjs-material-design-boilerplate/)

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