---
title: "ReactJS là gì và tại sao bạn nên tìm hiểu nó"
tags: [programming, reactjs, frontend]
categories: [programming]
share-img: /img/reactjs.jpg
---

**React** là một bộ thư viện giúp lập trình viên xây dựng giao diện web (user interface, hay UI) từ những thành phần nhỏ nhất gọi là **component**. Một *component* có thể hiểu như là hỗn hợp của mã HTML và JavaScript phục vụ cho việc hiển thị và xử lý logic của một thành phần nhỏ trong một màn hình UI hoàn chỉnh. Từ những *component* nhỏ đó, chúng ta có thể xây dựng được những màn hình UI rất phức tạp.

![](/img/reactjs.jpg)

# Một ví dụ đơn giản TodoList

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

Khi tìm hiểu một thư viện hay framework về UI, một ví dụ kinh điển đó là ứng dụng **to-do list**. Với ứng dụng này, chúng ta có thể có một *component* `Todo` với ReactJS như sau:

```
/**
 * An individual ToDo item
 * @param {Object}  props
 * @param {String}  props.todoItem  A ToDo
 */
const Todo = ({ todoItem }) => (
  <li>{ todoItem.text }</li>
);
```

Và một *component* `TodoList` chính là danh sách các `Todo`:

```
/**
 * A todoList with a Todo for each item in todoListData
 * @param {Object}          props
 * @param {Array.<String>}  props.todoListData A List of ToDos
 */
const TodoList = ({ todoListData }) => {
  const todoListItems = todoListData
    .map(todo => <Todo todo={todo} />);

  return <ul>{todoListItems}</ul>;
};
```

Đoạn code thứ nhất tạo ra một *function* `Todo`, và khi được chạy, nó sẽ sinh ra mã *HTML* `<li>` với thuộc tính `text` bên trong. Đoạn code thứ 2 tạo ra một mảng `Todo` với dữ liệu đầu vào là một mảng text, rồi chúng được cho vào bên trong thẻ *HTML* `<ul>`.

Hai đoạn code phía trên đều được viết với **JSX**, là một dạng syntax mở rộng của *JavaScript* giúp chúng ta mix *JavaScript* với *HTML*. Có thể tìm hiểu thêm về *JSX* [tại đây](https://reactjs.org/docs/introducing-jsx.html).

Cuối cùng, để dùng *component* `TodoList` ở trên:

```
const todos = [
  { text: "Chạy bộ 5km" },
  { text: "Về nhà nấu ăn" },
  { text: "Gọi điện cho bạn gái" }
];

const app = <TodoList todoListData={todos} />;
const targetDOMElement = document.getElementById("app-root");

ReactDOM.render(app, targetDOMElement);
```

Chúng ta sẽ có được mã *HTML* như sau khi được render:

```
<ul>
  <li>Chạy bộ 5km</li>
  <li>Về nhà nấu ăn</li>
  <li>Gọi điện cho bạn gái</li>
</ul​>
```

Có thể dễ nhận thấy trong ví dụ phía trên, đoạn code không thực sự xử lý hay thay đổi hiển thị của trang. Hai *component* `Todo` và `TodoList` đơn giản trả về code *HTML* dựa vào input được đưa vào. Tuy nhiên, khái niệm này là phần cốt lõi của *React*. *React developer* tạo ra các miếng ghép của *UI* tương tự như ví dụ ở trên, và truyền kết quả *HTML* tới một hàm `render` đặc biệt. Khi dữ liệu input thay đổi, ví dụ khi user thêm một item vào danh sách *to-do list*, thì sẽ không có bất kỳ đoạn code thêm nào chuyên cho việc update UI. Thay vào đó, dữ liệu mới sẽ được truyền vào *component* giống như khi page load lần đầu (*initial page load*), và ứng dụng sẽ render lại thành phần UI đó. Tính năng **re-render** này của React xem qua thì có vẻ như là một điểm trừ performance. Tuy nhiên, đây lại là một điểm tinh tế của React.

Khi hàm `render` được gọi lại, thay vì vẽ lại toàn bộ giao diện UI ngay lập tức, React sẽ so sánh kết quả mới có, với bản copy của kết quả trước đó. Dựa vào phần khác biệt, nó sẽ cố gắng để chỉ *render* phần thay đổi nhỏ nhất.

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

Quá trình so sánh giữa trạng thái mới (*new state*) với trạng thái trước đó (*last-known state*) diễn ra tự động. Điều này giúp cho developer dễ dàng thể hiện ứng dụng như họ mong muốn, đưa ra dữ liệu, mà không cần lo lắng quá trình xảy ra khi dữ liệu thay đổi. Style này được biết đến là **declarative programming**. Style này hiệu quả hơn **imperative programming**, là style khi lập trình ta cần khai báo đầy đủ cho một chương trình nên hoạt động như thế nào, và cần khai báo cả các bước cho hoạt động đó.

Có thể xem thêm ví dụ về React trên trang chủ, [Tutorial: Intro to React
](https://reactjs.org/tutorial/tutorial.html).

# React là một thư viện, không phải một framework

Một điểm cần chú ý để phân biệt React với các framework khác như Ember.js hay AngularJS đó là: React chỉ quan tâm đến việc render UI, mà không xử lý các tác vụ khác. Hiện tại, khi dùng React chúng ta có thể có các *stack* như sau:

**Application code**

React, Redux, react-router

**Build tools**

Webpack, Uglify, npm/yarn, Babel, babel-preset-env

**Test tools**

ESLint, Enzyme, Mocha/Jest

Một số cuốn sách mới xuất bản recommend về ReactJS:

Tiếng Anh:

<table border="0" cellpadding="0" cellspacing="0"><tr><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:310px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15178257%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18825554%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=18825554&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F3344%2F9781617293344.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F3344%2F9781617293344.jpg%3F_ex%3D300x300&s=300x300&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15178257%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18825554%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >React Quickly: Painless Web Apps with React, Jsx, Redux, and Graphql REACT QUICKLY [ Azat Mardan ]</a><br><span >価格：12096円（税込、送料無料)</span> <span style="color:#BBB">(2018/8/20時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td></tr></table>

Tiếng Nhật:

<table border="0" cellpadding="0" cellspacing="0"><tr><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:310px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15357492%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19012330%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=19012330&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F0490%2F9784839960490.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F0490%2F9784839960490.jpg%3F_ex%3D300x300&s=300x300&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15357492%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19012330%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >React開発　現場の教科書 [ 石橋啓太 ]</a><br><span >価格：3769円（税込、送料無料)</span> <span style="color:#BBB">(2018/8/20時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:310px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15299539%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18946423%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=18946423&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F3353%2F9784798153353.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F3353%2F9784798153353.jpg%3F_ex%3D300x300&s=300x300&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15299539%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18946423%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >React入門 React・Reduxの導入からサーバサイドレンダリングによるUXの向上まで （NEXT ONE） [ 穴井 宏幸 ]</a><br><span >価格：3218円（税込、送料無料)</span> <span style="color:#BBB">(2018/8/20時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td></tr></table>

<table border="0" cellpadding="0" cellspacing="0"><tr><td><div style="border:1px solid #000000;background-color:#FFFFFF;width:310px;margin:0px;padding-top:6px;text-align:center;overflow:auto;"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15084914%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18729166%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  ><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=18729166&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F0751%2F9784798050751.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F0751%2F9784798050751.jpg%3F_ex%3D300x300&s=300x300&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]"></a><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15084914%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F18729166%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIzMDB4MzAwIiwibmFtIjoxLCJuYW1wIjoiZG93biIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjB9" target="_blank" rel="nofollow" style="word-wrap:break-word;"  >作りながら学ぶReact入門 [ 吉田裕美 ]</a><br><span >価格：2160円（税込、送料無料)</span> <span style="color:#BBB">(2018/8/20時点)</span></p></div><br><p style="font-size:12px;line-height:1.4em;margin:5px;word-wrap:break-word"></p></td></tr></table>


