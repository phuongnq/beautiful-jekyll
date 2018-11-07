---
title: "【NodeJS】Dùng thử Apache Kafka cho hệ thống real-time data streaming"
tags: [programming, nodejs, javascript]
categories: [programming, vietnamese]
share-img: /img/kafka.png
---

# Giới thiệu

**Apache Kafka**, hay gọi đơn giản *Kafka* là một hệ thống stream phân tán. Điều này có nghĩa là gì?

![](/img/kafka.png)

**Một hệ thống stream có những đặc tính như sau:**

* Cơ chế publish/subscribe một stream messages. Cái này tương tự như là message queue.

* Có khả năng lưu trữ stream record chịu lỗi trong một khoảng thời gian

* Xử lý stream record theo thứ tự nó diễn ra

**Kafka được dùng chính với mục đích:**

* Xây một hệ thống real-time data pipeline để lấy dữ liệu giữa các hệ thống hoặc ứng dụng

* Xây dựng một hệ thống streaming real-time trao đổi/tương tác với dòng dữ liệu (*stream of data*)

**Một vài khái niệm cơ bản:**

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

* Kafka chạy như 1 cluster trên 1 hoặc nhiều server, có thể phân bố ra nhiều data center

* Dữ liệu lưu trữ trên Kafka gọi là *record* và phân chia theo *topic*

* Mỗi *record* sẽ có *key*, *value* và *timestamp*

**Các APIs chính:**

* *Producer API*: có nhiệm vụ sinh ra *record*, hiểu như là nhà xuất bản

* *Consumer API*: nhận *record* từ *Producer*, hiểu như là subscriber

* *Stream API*: hiểu như là bộ xử lý cho stream. Nhận input từ stream, xử lý và output ra stream khác

* *Connector API*: kết nối Kafka topics với ứng dụng hoặc cơ sở dữ liệu. Ví dụ: connector kết nối đến MySQL ghi bất kỳ thay đổi nào vào một bảng

Tìm hiểu thêm về *Kafka* trên trang chủ: https://kafka.apache.org/intro

# Implement

Dưới đây demo cài đặt *Kafka* server trên MacOS với `brew`, cách tạo *topic*, chạy thử *Producer*, *Consumer* và implement một *Consumer* đơn giản bằng NodeJS.

## Cài đặt Kafka với `brew`:

```bash
brew install kafka
```

Như hiện tại, lệnh này sẽ cài đặt cả *Kafka* và *ZooKeeper*.

Đường dẫn cài đặt:

* Kafka: `/usr/local/Cellar/kafka/2.0.0`

* Zookeeper: `/usr/local/Cellar/zookeeper/3.4.13`

Để chạy server:

Sửa file `/usr/local/etc/kafka/server.properties`, thêm dòng sau vào cuối:

```text
port = 9092
advertised.host.name = localhost
```

Khởi động *ZooKeeper*:

```bash
zkServer start
```

Khởi động *Kafka*:

```bash
 /usr/local/Cellar/kafka/2.0.0/bin/kafka-server-start  /usr/local/etc/kafka/server.properties
```

## Tạo thử topic

Với *Kafka server* đang chạy như trên, mở một *terminal* khác, chạy lệnh:

```bash
/usr/local/Cellar/kafka/2.0.0/bin/kafka-topics  --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic a_test_topic
```

Nếu không có lỗi gì, output sẽ là:

```bash
WARNING: Due to limitations in metric names, topics with a period ('.') or underscore ('_') could collide. To avoid issues it is best to use either, but not both.
Created topic "a_test_topic".
```

Như vậy thì *topic* đã được tạo thành công

## Gửi message từ Producer

Với *Kafka server* đang khởi động như trên, chạy lệnh sau trên một terminal mới:

```bash
/usr/local/Cellar/kafka/2.0.0/bin/kafka-console-producer --broker-list localhost:9092 --topic a_test_topic
```

Khi này *Producer* sẽ khởi động và chúng ta có thể gõ bất kỳ *message* nào dưới dạng text.

## Nhận message từ Comsumer

Với *Kafka server* & *Producer* đang chạy như trên, mở một *terminal* mới, chạy lệnh:

```bash
/usr/local/Cellar/kafka/2.0.0/bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic a_test_topic --from-beginning
```

Lệnh này sẽ cho chạy *Consumer*, mỗi khi có message mới gõ từ terminal của *Producer*, message này cũng sẽ hiện ra ở *terminal* của *Consumer*.

## Implement Consumer với NodeJS

Bản implement *Consumer* này dùng thư viện: https://github.com/SOHU-Co/kafka-node

Cài gói thư viện với lệnh:

```bash
npm init -y
npm install --save kafka-node
```

Tạo một file `consumer.js` với nội dung:

```javascript
const kafka = require('kafka-node');

const { Consumer, Offset, Client } = kafka;

const topic = 'a_test_topic';

const client = new Client();

const topics = [{
    topic,
}];

const options = {
    autoCommit: false,
    fetchMaxWaitMs: 1000,
    fetchMaxBytes: 1024 * 1024
};

const consumer = new Consumer(client, topics, options);
const offset = new Offset(client);

consumer.on('message', (message) => {
    console.log(message);
});

consumer.on('error', (err) => {
    console.log('error', err);
});

/*
* If consumer get `offsetOutOfRange` event, fetch data from the smallest(oldest) offset
*/
consumer.on('offsetOutOfRange', (_topic) => {
    const t = _topic;
    t.maxNum = 2;

    offset.fetch([topic], (err, offsets) => {
        if (err) {
            console.error(err);
            return;
        }
        const min = Math.min.apply(null, offsets[t.topic][t.partition]);
        consumer.setOffset(t.topic, t.partition, min);
    });
});
```

Chạy với lệnh:

```bash
node consumer.js
```

Mỗi khi có message mới từ *Producer* thì *message* này cũng hiện ra ở màn hình của *NodeJS client*. Ví dụ:

```text
{ topic: 'a_test_topic',
  value: 'Hello world',
  offset: 1,
  partition: 0,
  highWaterOffset: 10,
  key: null }
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

Một vài tài liệu có thể tham khảo khi tìm hiểu về Kafka:

* Trang chủ: [Apache Kafka](https://kafka.apache.org/)

* Sách tiếng Anh:

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1491936169&asins=1491936169&linkId=91a440871788712e63db11f247915a15&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066c0&bg_color=ffffff">
</iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ac&ref=qf_sp_asin_til&ad_type=product_link&tracking_id=phuongnq-20&marketplace=amazon&region=US&placement=1617294470&asins=1617294470&linkId=e0a9b81440e2fd37b7dd649eef702970&show_border=false&link_opens_in_new_window=false&price_color=333333&title_color=0066c0&bg_color=ffffff">
</iframe>

* Sách tiếng Nhật:

<table>
    <tr>
        <td style="width:128px">
            <a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15634554%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19325731%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIxMjh4MTI4IiwibmFtIjoxLCJuYW1wIjoicmlnaHQiLCJjb20iOjEsImNvbXAiOiJkb3duIiwicHJpY2UiOjEsImJvciI6MSwiY29sIjoxLCJiYnRuIjoxfQ%3D%3D" target="_blank" rel="nofollow" style="word-wrap:break-word;"><img src="https://hbb.afl.rakuten.co.jp/hgb/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?me_id=1213310&item_id=19325731&m=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F2370%2F9784798152370.jpg%3F_ex%3D80x80&pc=https%3A%2F%2Fthumbnail.image.rakuten.co.jp%2F%400_mall%2Fbook%2Fcabinet%2F2370%2F9784798152370.jpg%3F_ex%3D128x128&s=128x128&t=picttext" border="0" style="margin:2px" alt="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]" title="[商品価格に関しましては、リンクが作成された時点と現時点で情報が変更されている場合がございます。]">
            </a>
        </td>
        <td style="vertical-align:top;width:136px;"><p style="font-size:12px;line-height:1.4em;text-align:left;margin:0px;padding:2px 6px;word-wrap:break-word"><a href="https://hb.afl.rakuten.co.jp/hgc/16f3ccdb.b7f9e219.16f3ccdc.8757d2f7/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F15634554%2F&m=http%3A%2F%2Fm.rakuten.co.jp%2Fbook%2Fi%2F19325731%2F&link_type=picttext&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJwaWN0dGV4dCIsInNpemUiOiIxMjh4MTI4IiwibmFtIjoxLCJuYW1wIjoicmlnaHQiLCJjb20iOjEsImNvbXAiOiJkb3duIiwicHJpY2UiOjEsImJvciI6MSwiY29sIjoxLCJiYnRuIjoxfQ%3D%3D" target="_blank" rel="nofollow" style="word-wrap:break-word;">Apache Kafka 分散メッセージングシステムの構築と活用 （NEXT ONE） [ 株式会社NTTデータ ]</a><br><span >価格：3888円（税込、送料無料)</span> <span style="color:#BBB">(2018/11/7時点)</span></p>
        </td>
    </tr>
</table>