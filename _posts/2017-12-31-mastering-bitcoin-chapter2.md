---
title: Làm chủ bitcoin - Chương 2
date: 2017-12-31 16:06:00
tags: [mastering bitcoin, vietnamese, book, translate]
---
## Giao dịch, block, mining và blockchain

Không giống như hệ thống ngân hàng hay hệ thống thanh toán truyền thống, hệ thống bitcoin hoàn toàn dựa vào sự tin tưởng phân tán. Thay vì dựa vào sự tin tưởng của chính quyền tập trung, đối với bitcoin thì sự tin tưởng nổi bật lên từ tương tác giữa những người tham gia khác nhau trong hệ thống. Trong chương này, chúng ta sẽ khảo sát bitcoin từ cái nhìn bậc cao bằng việc giám sát một giao dịch đơn lẻ trong hệ thống và xem xem nó trở lên "đáng tin" như thế nào, và làm thế nào nó được chấp nhận bởi sự thỏa thuận phân tán của cơ chế bitcoin, cũng như việc cuối cùng nó được ghi lại vào blockchain, chính là sổ cái của mọi giao dịch. Các chương tiếp theo sẽ nghiên cứu đào sâu về công nghệ đằng sau giao dịch, mạng lưới và việc đào bitcoin.

### Sơ lược về bitcoin

Trong biểu đồ sơ lược bên dưới, chúng ta thấy được rằng hệ thống bitcoin gồm có: người dùng với ví có chứa khóa, các giao dịch được sinh ra trong mạng lưới và miner là những người tạo ra (thông qua cạnh tranh tính toán máy tính) sự thỏa thuận blockchain, thứ là sổ cái chính thức cho mọi giao dịch.

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0201.png" style="width: 100%;" alt="Sơ lược bitcoin"/>
</div>

Một số **blockchain explorer** gồm có:

* [Bitcoin Block Explorer](https://blockexplorer.com/)
* [BlockCypher Explorer](https://live.blockcypher.com/)
* [blockchain.info](https://blockchain.info/)
* [BitPay Insight](https://insight.bitpay.com/)

Mỗi trang web ở trên đều có chức năng tìm kiếm có thể tìm từ địa chỉ bitcoin, hash của giao dịch, số block, hoặc block hash và trả lại thông tin tương ứng từ mạng lưới bitcoin. Với mỗi ví dụ về giao dịch hoặc block, chúng tôi sẽ cung cấp một URL để bạn có thể tự học và tìm hiểu.

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

### Mua một cốc cà phê
Alice, người được giới thiệu ở chương trước, là một người dùng mới và cô đã có được bitcoin đầu tiên. Như chúng ta đã biết trong phần trước, Alice gặp bạn của mình là Joe và đổi tiền mặt lấy bitcoin. Giao dịch được tạo ra bởi Joe, và số tiền gửi vào ví của Alice là 0.10 BTC. Bây giờ Alice sẽ thực hiện giao dịch đầu tiên, mua một cốc cà phê từ quán của Bob ở Palo Alto, California.

Quán cà phê của Bob gần đây chấp nhận thanh toán bitcoin bằng việc thêm lựa chọn đó vào hệ thống *point-of-sale*. Giá ở quán được liệt kê bằng đồng tiền USD, tuy nhiên tại quầy thanh toán, người dùng có thể lựa chọn trả bằng USD hoặc bằng bitcoin. Alice gọi một cốc cà phê và để thực hiện giao dịch thì Bob chỉ cần nhập nó vào máy. Hệ thống *point-of-sale* sẽ tự động đổi giá từ USD sang bitcoin với tỷ giá hiện tại của thị trường và hiển thị kết quả bằng cả 2 đồng tiền:

```
Total:
$1.50 USD
0.015 BTC
```

Bob nói: "Tổng giá là 1.5 đô, hoặc 15 millibits."

Hệ thống *point-of-sale* của Bob tự động tạo ra một mã QR đặc biệt chứa lệnh thanh toán (xem mã QR thanh toán).

Không giống như mã QR thông thường chỉ chứa địa chỉ bitcoin của bên nhận, một lệnh thanh toán là một địa chỉ URL được mã hóa thành QR chứa địa chỉ nhận, tổng giá trị thanh toán, và một mô tả thông thường cho nội dung thanh toán, như là "Quán cà phê của Bob". Điều này cho phép ứng dụng ví bitcoin điền trước những thông tin cần thiết cho thanh toán đồng thời cũng chỉ cho người dùng thông tin mà con người có thể đọc được. Bạn có thể quét mã QR với một ứng dụng ví bitcoin nào đó để biết được Alice thấy những thông tin gì.

<div style="text-align: left;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0202.png" style="height: 100%;" alt="Mã QR lệnh thanh toán"/>
</div>

Tip:
> Thử quét mã này từ ví của bạn để thấy địa chỉ và số lượng, nhưng chú ý *KHÔNG GỬI TIỀN THẬT*.

Mã QR cho lệnh thanh toán mã hóa URL như sau, được định nghĩa trong BIP-21:

```
bitcoin:1GdK9UzpHBzqzX2A9JFP3Di4weBwqgmoQA?
amount=0.015&
label=Bob%27s%20Cafe&
message=Purchase%20at%20Bob%27s%20Cafe

Nội dung của URL:

Một địa chỉ bitcoin: "1GdK9UzpHBzqzX2A9JFP3Di4weBwqgmoQA"
Lượng thanh toán: "0.015"
Nhãn cho bên nhận: "Bob's Cafe"
Một mô tả cho thanh toán: "Purchase at Bob's Cafe"
```

Alice dùng smartphone của mình để quét mã vạch trên màn hình. Smartphone của cô hiển thị thanh toán 0.0150 BTC tới quán cà phê của Bob, và cô chọn *send* để thực hiện thanh toán. Trong vài giây (bằng với thời gian cấp phép của thẻ tín dụng), Bob nhìn thấy thanh toán trên màn hình, hoàn tất giao dịch.


Trong phần kế tiếp, chúng ta sẽ xem xét kỹ lưỡng giao dịch này. Chúng ta sẽ xem ví của Alice cấu hình như thế nào, làm thế nào để phát tán ra mạng lưới, nó được kiểm nghiệm như thế nào, và cuối cùng, làm thế nào Bob có thể dùng giá trị nhận được trong các giao dịch kế tiếp.

Tip

> Mạng lưới bitcoin có thể thực hiện giao dịch nhỏ hơn 1, ví dụ từ millibitcoin (1/1000 bitcoin) cho tới 1/100,000,000 bitcoin, là giá trị của một **satoshi**. Trong cuốn sách này thì chúng ta sẽ dùng từ "bitcoin" để chỉ bất kỳ một lượng giá trị bitcoin nào, từ đơn vị nhỏ nhất (1 satoshi) cho tới tổng tất cả số bitcoin chúng ta có thể đào được (21,000,000).

Bạn có thể kiểm chứng giao dịch của Alice tới quán cà phê của Bob trên blockchain bằng việc dùng **block explorer** (Xem giao dịch của Alice trên blockexplorer.com):

Ví dụ 1. Xem giao dịch của Alice trên blockexplorer.com
```
https://blockexplorer.com/tx/0627052b6f28912f2703066a912ea577f2ce4da4caa5a5fbd8a57286c345c2f2
```

## Giao dịch bitcoin

Nói một cách đơn giản thì một giao dịch nói cho mạng lưới biết rằng người chủ sở hữu **giá trị** bitcoin đã chấp thuận gửi **giá trị** đó tới một người chủ sở hữu khác. Người sở hữu mới này có thể dùng lượng bitcoin này cho một giao dịch khác tới một người chủ sở hữu khác, và tiếp tục như vậy, tạo nên chuỗi quyền sở hữu (*chain of ownership*).

### input và output của giao dịch

Giao dịch cũng giống như những dòng trong sổ cái ghi chép kế toán kép. Mỗi giao dịch chứa một hoặc nhiều "input", điều này cũng giống như việc ghi nợ cho một tài khoản bitcoin. Tại phía bên kia của các giao dịch, có một hoặc nhiều "output", giống như là việc thêm tín dụng vào một tài khoản bitcoin. Tổng input và output (ghi nợ và thêm tín dụng) không nhất thiết phải bằng nhau. Thay vào đó, tổng output thường ít hơn input một chút, độ chênh lệch này đại diện cho phí giao dịch. Phí này là một phần nhỏ trả cho miner, những người có công thêm giao dịch vào sổ cái. Một giao dịch bitcoin được hiển thị như một entry sổ cái ghi chép trong phần Transaction giống như ghi chép kế toán kép.

Giao dịch cũng chứa bằng chứng sở hữu (*proof of ownership*) cho mỗi một lượng **giá trị** bitcoin (input) dưới dạng chữ ký điện tử từ người chủ, được **sử dụng**. Và nó có thể được kiểm tra lại một cách độc lập từ bất kỳ ai. Theo cách nói của bitcoin, "sử dụng" nghĩa là ký vào một giao dịch để chuyển *giá trị* từ một giao dịch trước đó tới một chủ sở hữu mới được định danh bởi địa chỉ bitcoin.

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0203.png" style="width: 100%;" alt="Giao dịch giống như là sổ kế toán kép"/>
</div>

### Chuỗn giao dịch (transaction chain)

Thanh toán của Alice cho cửa hàng cà phê của Bob dùng output của giao dịch trước đó làm input cho giao dịch hiện tại. Trong chương trước, Alice đã trả tiền mặt để nhận được bitcoin từ bạn mình là Joe. Giao dịch đó tạo ra một *giá trị* bitcoin và được khóa bằng **khóa** của Alice. Giao dịch mới của Alice tới quán cà phê của Bob tham chiếu đến giao dịch trước đó lấy làm input và tạo ra output mới để trả cho cốc cà phê đồng thời nhận lại tiền thừa. Những giao dịch như vậy tạo ra một chuỗi (chain), nơi mà input từ giao dịch gần đây nhất tương đương với output từ giao dịch trước đó. *Khóa* của Alice ký nhận để mở khóa output của những giao dịch trước đó, do vậy chứng thực với mạng lưới rằng cô sở hữu khoản tài chính. Cô gắn thanh toán của cốc cà phê tới địa chỉ của Bob, do đó "gây cản trở" đến output đó với yêu cầu là Bob tạo ra chữ ký để sử dụng lượng bitcoin đó. Điều này là kết quả của giao dịch một *giá trị* giữa Alice và Bob. Chuỗi những giao dịch này, từ Joe tới Alice rồi tới Bob, được miêu tả như là một *chuỗi* giao dịch, nơi mà output từ một giao dịch sẽ là input cho giao dịch kết tiếp.

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0204.png" style="width: 100%;" alt="Một chuỗi giao dịch, output của giao dịch này là input của giao dịch kế tiếp"/>
</div>

### Tạo chuỗi (chain)

Nhiều giao dịch bitcoin sẽ gồm có output mà tham chiếu đến cả địa chỉ của chủ sở hữu mới và địa chỉ của chủ sở hữu hiện tại, được gọi là địa chỉ hoàn lại (change address). Điều này là do input của giao dịch, cũng giống như tờ tiền giấy, không thể chia làm đôi. Nếu bạn mua một sản phẩm với giá $5 USD tại một cửa hàng nhưng dùng đồng mệnh giá $20 USD thì sẽ nhận lại $15 USD tiền hoàn lại. Ý tưởng này cũng được áp dụng cho input giao dịch bitcoin. Nếu bạn mua một sản phẩm có giá 5 bitcoin nhưng chỉ có input là 20 bitcoin, bạn sẽ gửi một output là 5 bitcoin tới chủ cửa hàng và một output là 15 bitcoin trở lại địa chỉ ví của bạn như là tiền hoàn lại (trừ đi khoản phí giao dịch). Điều quan trọng ở đây là, địa chỉ hoàn lại (change address) không nhất thiết phải giống với địa chỉ input, và trên thực tế do lý do bảo mật, nó thường là một địa chỉ mới cho ví của chủ sở hữu.

Mỗi loại ví khác nhau thường có những chiến thuật khác nhau khi tập hợp input để tạo lệnh thanh toán cho người dùng. Chúng có thể tập hợp nhiều input nhỏ, hoặc dùng một input to hơn có giá trị bằng hoặc lớn hơn giá trị cần thanh toán. Trừ khi ví có thể tập hợp input để tạo ra một *giá trị* vừa đủ với giá trị cần thanh toán cộng thêm phí phát sinh, thì ví sẽ cần phải tạo ra sự hoàn lại (change). Điều này cũng rất giống như việc chúng ta sử dụng tiền mặt. Nếu lúc nào cũng dùng tờ tiền mệnh giá lớn nhất trong túi, bạn sẽ nhận lại rất nhiều tiền thừa trong túi của mình. Nếu chỉ dùng tiền lẻ, trong túi bạn lúc nào cũng còn lại những tờ tiền mệnh giá lớn. Người ta thường tìm ra một công thức cân bằng giữa hai cách dùng này một cách vô ý thức. Và lập trình viên cho ví bitcoin cũng áp dụng phương thức này để lập trình sự cân bằng đó.

Để tổng hợp lại: giao dịch di chuyển **giá trị** từ input sang output. Một input chính là tham chiếu của một output của giao dịch trước đó, giúp chúng ta chỉ ra từ đâu mà *giá trị* đó tới. Một giao dịch output truyền một **giá trị** nhất định tới địa chỉ bitcoin của chủ sở hữu mới và đồng thời có thể tạo ra output hoàn lại (change output) về cho chủ sở hữu ban đầu. Output từ một giao dịch có thể dùng như input của một giao dịch mới, do đó tạo ra một chuối chủ sở hữu (chain of ownership) khi mà **giá trị** được di chuyển giữa các chủ sở hữu.

### Các dạng giao dịch thông thường

Dạng giao dịch thông thường nhất là việc thanh toán từ một địa chỉ tới một địa chỉ khác, và thường phát sinh "tiền thừa" trở lại cho chủ sở hữu ban đầu. Loại giao dịch này có 1 input và 2 output:

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0205.png" style="width: 100%;" alt="Giao dịch thông dụng">
</div>


Một dạng giao dịch thông dụng khác nữa là tổng hợp của vài input để tạo ra một output duy nhất. Điều này cũng giống như việc đổi tiền trên thực tế, đổi nhiều đồng tiền nhỏ để lấy một tờ tiền to duy nhất. Những giao dịch như vậy thi thoảng được tạo ra bởi ứng dụng ví để làm sạch nhiều *lượng* nhỏ bitcoin sinh ra từ *tiền thừa* của các giao dịch thanh toán trước đó.

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0206.png" style="width: 100%;" alt="Giao dịch tổng hợp nguồn tài chính">
</div>


Cuối cùng, một dạng giao dịch khác nữa có thể bắt gặp từ một sổ bitcoin lớn, giao dịch phân phát 1 input tới nhiều output, đại diện cho nhiều người nhận. Giao dịch này thỉnh thoảng được dùng bởi các đơn vị thương mại để phân phối nguồn tài chính, như là trả tiền cho nhiều nhân viên.

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0207.png" style="width: 100%;" alt="Giao dịch phân phối nguồn tài chính">
</div>

### Tạo một giao dịch

Ứng dụng ví của Alice chứa đựng đủ logic để lựa chọn input, output thích hợp nhằm mục đích tạo giao dịch theo như chỉ định của Alice. Alice chỉ cần chỉ định một đích đến và một *giá trị* cho giao dịch, phần còn lại sẽ được thực hiện bởi ứng dụng ví mà cô không cần phải bận tâm chi tiết bên trong. Đặc biệt, ứng dụng ví có thể xây dựng giao dịch ngay cả khi nó hoàn toàn trong trạng thái offline. Cũng giống như việc chúng ta ký vào tờ séc tại nhà, rồi gửi tới ngân hàng bằng một chiếc phong bì, giao dịch bitcoin cũng không nhất thiết phải được xây dựng và ký khi đang trong trạng thái kết nối với mạng lưới bitcoin.

### Lựa chọn input hợp lý

Ứng dụng ví của Alice ban đầu sẽ phải chọn ra input hợp lý để trả cho Bob. Phần lớn ví sẽ tính toán ra tất cả output thuộc sở hữu của những địa chỉ trong ví mà có thể dùng được. Do đó, ví của Alice sẽ chứa một bản copy output giao dịch từ Joe (là giao dịch đổi tiền mặt lấy bitcoin). Một ứng dụng ví bitcoin chạy full-node thường chứa bản copy cho mọi output kể cả không được thực sự gửi đi cho mọi giao dịch trong blockchain. Điều này cho phép ví có thể cấu hình input cho giao dịch cũng như có thể nhanh chóng xác nhận những giao dịch đang được chuyển đến xem có đúng input không. Tuy nhiên, Một client full-node thường chiếm rất nhiều không gian ổ cứng nên các ví thông thường dùng loại "lightweight" client, chỉ lưu trữ những output không được gửi đi sở hữu bởi người dùng đó.

Nếu như ứng dụng ví không lưu trữ copy của output không được gửi đi của các giao dịch (unspend output), nó có thể query từ bitcoin network để nhận được thông tin này dùng nhiều APIs khác nhau cung cấp bởi bên provider hoặc bằng cách dùng API gọi đến ứng dụng full-node. Việc tra cứu tất cả output không được gửi đi từ địa chỉ của Alice được thực hiện bằng request API, là một lệnh `HTTP GET` tới một địa chỉ *URL* được chỉ định. Địa chỉ *URL* này sẽ trả về tất cả output không được gửi đi của một giao dịch cho một địa chỉ, cho phép bất kỳ ứng dụng nào thông tin mà nó cần để xây dựng input cho những giao dịch kế tiếp. Chúng ta có thể dùng client HTTP command-line `cURL` để thực hiện việc này.

Ví dụ 2: Tra cứu tất cả output không được gửi đi từ địa chỉ của Alice

```
$ curl https://blockchain.info/unspent?active=1Cdid9KFAaatwczBwBttQcwXYCpvK8h7FK
```

```
{

	"unspent_outputs":[

		{
			"tx_hash":"186f9f998a5...2836dd734d2804fe65fa35779",
			"tx_index":104810202,
			"tx_output_n": 0,
			"script":"76a9147f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a888ac",
			"value": 10000000,
			"value_hex": "00989680",
			"confirmations":0
		}

	]
}
```

Response cho việc tra cứu tất cả output không được gửi đi (unspend output) cho địa chỉ ví bitcoin của Alice gồm duy nhất 1 unspend output (cái mà vẫn chưa được thực hiện) dưới quyền sở hữu là địa chỉ của Alice `1Cdid9KFAaatwczBwBttQcwXYCpvK8h7FK`. Response này chứa tham chiếu tới giao dịch mà có output không được gửi đi bao gồm (thanh toán từ Joe) và giá trị của nó bằng đơn vị *satoshis*, 10 million, tương đương 0.10 bitcoin. Với thông tin này, ứng dụng ví của Alice xây dựng một giao dịch để gửi *giá trị* đó tới địa chỉ của chủ mới.

Tip
> Xem chi thiết [giao dịch](https://blockchain.info/tx/7957a35fe64f80d234d76d83a2a8f1a0d8149a41d81de548f0a65a8a999f6f18) từ Joe đến Alice.

Như chúng ta có thể thấy, ví của Alice chứa đựng đủ bicoin trong 1 unspend output duy nhất để trả cho cốc cà phê. Nếu không làm được như vậy, ứng dụng ví của Alice có thể đã phải "rà soát" tất cả các lượng nhỏ unspend output, cũng giống như việc lượm đồng xu từ ví cho tới khi đủ tiền trả cho một cốc cà phê. Cả hai trường hợp đều có thể cần phải có một chút tiền thừa trả lại. Chúng ta sẽ thấy điều này trong phần tiếp theo, khi mà ứng dụng ví tạo output cho giao dịch (thanh toán).

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

### Tạo output

Output cho một giao dịch được tạo ra dưới dạng script mà tạo ra *trở ngại* trên một **giá trị** và chỉ có thể thực hiện bằng việc đưa ra lời giải cho script đó. Nói một cách đơn giản, output của giao dịch của Alice chứa một script diễn tả thứ giống như là "Output này có thể dùng để thanh toán cho bất kỳ ai có thể đưa ra chữ ký từ khóa tương đương như địa chỉ public của Bob". Bởi vì chỉ có Bob có ví với khóa tương tương cho địa chỉ đó, chỉ có ví của Bob là có khả năng đưa ra chữ ký để thực thi output này. Alice do đó sẽ làm "trở ngại" giá trị output với yêu cầu chữ ký từ Bob.

Giao dịch này cũng sẽ bao gồm một output thứ hai, bởi quỹ tiền của Alice dưới dạng 0.10 BTC output, nhiều hơn số tiền cần thiết cho một cốc cà phê là 0.015 BTC. Alice sẽ cần có 0.085 BTC tiền thừa. Thanh toán trả lại tiền thừa cho Alice cũng được tạo bởi chính ví của Alice, output tương tự như giao dịch thanh toán cho Bob. Về bản chất thì ví của Alice chia quỹ tiền của cô thành 2 thanh toán: một thanh toán cho Bob và một trả lại cho cô. Sau đó cô có thể dùng (spend) output của tiền thừa này cho một giao dịch tiếp theo đó.

Cuối cùng, giao dịch sẽ được thực thi bởi network đúng lúc, ứng dụng ví của Alice sẽ thêm một chút phí. Điều này không nhất thiết hiện hữu trong giao dịch; nó được thể hiện bởi giá trị khác nhau giữa input và output. Thay vì nhận 0.085 BTC tiền thừa, Alice tạo ra chỉ 0.0845 BTC là output thứ hai, và sẽ có 0.0005 BTC (một nửa của millibitcoin) còn lại. 0.10 BTC input không thực sự spend cho 2 output, bởi tổng của chúng ít hơn so với giá trị 0.10. Phần khác nhau này là phí được thu thập bởi miner, là phí cho việc công nhận và thêm giao dịch vào một *block* để ghi vào blockchain.

Kết quả của giao dịch có thể được thấy dùng ứng dụng web *blockchain explorer*, biểu diễn giao dịch từ Alice tới quán cà phê của Bob.

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0208.png" style="width: 100%;" alt="Giao dịch từ Alice tới quán cà phê của Bob"/>
</div>

Tip
> Xem [Giao dịch từ Alice tới quán cà phê của Bob](https://blockchain.info/tx/0627052b6f28912f2703066a912ea577f2ce4da4caa5a5fbd8a57286c345c2f2)

### Thêm giao dịch vào sổ cái

Giao dịch được tạo bởi ứng dụng ví của Alice có độ dài **258 bytes** và chứa đựng đầy đủ thông tin cần thiết để xác nhận quyền sở hữa của quỹ tiền và chuyển nhượng cho chủ sở hữu mới. Bây giờ, giao dịch phải được truyền đi tới mạng bitcoin network nơi mà nó có thể trở thành một phần của blockchain. Trong phần tiếp theo chúng ta sẽ thấy được làm thế nào giao dịch có thể trở thành một phần của block mới và làm thế nào block đó có thể được "mining". Cuối cùng, chúng ta sẽ thấy được làm thế nào một block mới, sau khi đã được thêm vào blockchain, có thể tăng tăng được độ tin cậy bở network khi nhiều block khác được thêm vào.

**Truyền một giao dịch**

Bởi vì giao dịch đã chứa đủ thông tin cần thiết để xử lý, việc nó truyền đi như thế nào và truyền đi ở đâu tới bitcoin network là không quan trọng. Mạng lưới bitcoin network là một mạng peer-to-peer, mỗi bitcoin client tham gia bằng việc kết nối tới vài bitcoin client khác. Mục đích của bitcoin network là để truyền đi các giao dịch và block tới những người tham gia.

**Làm thế nào để truyền đi**

Bất kỳ một hệ thống nào, ví dụ như server, ứng dụng desktop, hoặc ví mà tham gia vào bitcoin network bằng việc "dùng" bitcoin protocol thì được gọi là một bitcoin node. Ứng dụng ví của Alice có thể gửi một giao dịch mới tới bất kỳ bitcoin node nào bởi các kiểu kết nối: mạng dây, WiFi, mobile, vân vân. Ví bitcoin của cô không nhất thiết phải kết nối trực tiếp đến ví của Bob và cô không phải dùng mạng internet của quán cà phê, mặc dù cả 2 phương án đó đều có thể dùng được. Bất kỳ một node nào nhận được một giao dịch hợp lệ mà nó chưa từng thấy trước đó sẽ lập tức forward tới các node khác nó kết nối, một kỹ thuật truyền đi được gọi là **flooding**. Do đó, giao dịch nhanh chóng được phát sinh trong mạng peer-to-peer, đạt được một lượng lớn % các node kết nối trong vài giây.

** Nhìn từ phía Bob**

Nếu như ví bitcoin của Bob kết nối trực tiếp tới ứng dụng ví của Alice, ứng dụng ví của Bob có thể đã là node đầu tiên nhận được giao dịch. Tuy nhiên, ngay cả khi ví của Alice gửi giao dịch tới một ví khác thì nó cũng sẽ truyền tới Bob trong vài giây. Ví của Bob sẽ ngay lập tức xác nhận giao dịch của Alice như là thanh toán đang chờ bởi vì nó chứa output có thể thực thi dùng khoá của Bob. Ứng dụng ví của Bob cũng có thể xác nhận một cách độc lập rằng giao dịch được định hình hoàn chỉnh, dùng unspend input từ giao dịch trước, và chứa đựng đầy đủ phí giao dịch để thêm vào block tiếp theo. Tại thời điểm này Bob có thể giả định rằng giao dịch sẽ sớm được thêm vào block và được xác nhận với rất ít rủi ro.

Tip
> Một trong những nhận thức sai về giao dịch bitcoin là nó phải được "xác nhận" bằng cách đợi 10 phút cho mỗi block mới, hoặc có thể lên tới 60 phút cho việc xác nhận 6 giao dịch. Mặc dù việc xác nhận đảm bảo cho một giao dịch đã được chấp nhận bởi toàn bộ network, khoảng thời gian đợi dài như vậy là không cần thiết cho những giao dịch nhỏ như một cốc cà phê. Một cửa hàng có thể chấp nhận một giao dịch với giá trị nhỏ mà không cần xác nhận gì thêm, với rủi ro không nhiều hơn so với việc dùng thẻ tín dụng để tạo thanh toán mà không có giấy tờ ID tuỳ thân hoặc chữ ký, như việc các cửa hàng vẫn chấp nhận hàng ngày hiện tại.

### Đào bitcoin

Giao dịch của Alice bây giờ đã được truyền đi trong bitcoin network. Nó vẫn chưa thực sự là một phần của blockchain cho tới khi nó được xác thực và thêm vào một block bởi quá trình gọi là mining. Xem phần [mining] để biết thêm chi tiết thông tin.

Sự tin tưởng trong hệ thống bitcoin dựa trên tính toán máy tính. Giao dịch được gói lại bên trong các block, thứ cần một lượng nhất định tính toán để chứng minh, nhưng chỉ cần một lượng nhỏ tính toán máy tính để xác minh. Quá trình mining gồm 2 mục đích:

* Mining node xác nhận tất cả giao dịch bằng cách tham chiếu tới những luật nhất trí. Do đó, mining cung cấp độ bảo mật cho giao dịch bitcoin và đồng thời loại bỏ những giao dịch bị lỗi hoặc không hợp lệ.

* Mining tạo ra bitcoin mới cho mỗi block, giống như việc ngân hàng trung tâm in tiền mới. Số lượng bitcoin được tạo mới cho mỗi block là giới hạn và giảm theo thời gian, theo một kế hoạch cấp phát cố định.

Mining đạt được sự cân đối giữa chi phí bỏ ra và phần thưởng. Mining dùng tài nguyên điện để giải quyết vấn đề toán học. Một miner thành công sẽ thu thập phần thưởng là một bitcoin mới và phí giao dịch. Tuy nhiên, phần thưởng chỉ được thu thập nếu như miner đã xác thực đúng đắn tất cả giao dịch, đáp ứng quy luật về sự nhất trí. Sự cống hiến cân bằng này cung cấp tính bảo mật cho bitcoin mà không cần bất kỳ một cơ quan trung ương nào.

Một cách tốt để mô tả công việc mining là so sánh giống như một game sudoku lớn, cạnh tranh được thiết lập lại mỗi khi một người chơi giải được và độ khó được thiết lập sao cho nó mất khoảng 10 phút để tìm ra lời giải. Hãy tưởng tượng một câu đố sudoku lớn, với vài nghìn hàng và cột. Nếu đưa ra một câu đố đơn giản thì bạn có thể xác nhận lời giải nhanh chóng. Tuy nhiên, nếu như câu đố có một số ít ô vuông được điền và số còn lại được để trống không, công việc sẽ khó hơn rất nhiều! Độ khó của sudoku có thể được điều chỉnh bằng việc thay đổi kích cỡ của nó (nhiều hơn hay ít hơn số hàng và cột), tuy nhiên nó cũng có thể được xác nhận khá dễ dàng kể cả khi nó rất lớn. "Câu đố" được dùng trong bitcoin là một hash mật mã và biểu diễn tính chất tương tự: Nó không đối xứng khi mà khó có thể giải được nhưng dễ để xác nhận, và độ khó có thể điều chỉnh được.

Trong phần [câu chuyện người dùng], chúng ta đã giới thiệu về Jing, một nhà khởi nghiệp tại Thượng Hải. Jing chạy mining farm, là một business có thể chạy hàng nghìn máy tính mining, đua tranh để nhận phần thưởng là bitcoin. Cứ mỗi 10 phút hoặc tương tự như vậy, máy mining của Jing đua với hàng nghìn hệ thống tương tự trên toàn cầu để tìm ra lời giải cho một block giao dịch. Để tìm lời giải như vậy, thứ mà chúng ta gọi là Proof-of-Work (PoW), cần tới hàng quadrillion lệnh hash trên mỗi giây trên toàn bộ bitcoin network. Thuật toán cho Proof-of-Work bao gồm việc hash lặp đi lặp lại header của block và một số ngẫu nhiên với thuật toán mã hoá **SHA256** cho tới khi một lời giải match với một pattern được định sẵn. Miner đầu tiên tìm ra lời giải đó thắng ván chơi đó và xuất bản block vào blockchain.

Jing bắt đầu việc mining từ năm 2010 sử dụng một máy tính desktop để tìm ra Proof-of-Work phù hợp cho những block mới. Khi mà ngày càng có nhiều miner tham gia vào bitcoin network, độ khó của bài toán ngày càng tăng lên một cách nhanh chóng. Kết quả là Jing và nhiều miner khác phải nâng cấp phần cứng mạnh hơn nữa, ví dụ như với GPUs mạnh hơn, giống như card được dùng để chơi game desktop hoặc console. Tại thời điểm viết cuốn sách này, độ phức tạp đã rất cao đến mức chỉ sinh ra được lợi nhuận cho những miner chạy vi mạch đặc biệt ASIC (application-specific integrated circuits), về bản chất là hàng trăm thuật toán mining được đặt trong phần cứng, chạy song song trên một chip silicon đơn nhất. Công ty của Jing cũng tham gia vào mining pool, cũng giống như một tổ hợp quay xổ số cho phép nhiều người chơi chia sẻ nỗ lực và phần thưởng của họ. Công ty của Jing hiện tại chạy một nhà kho chứa hàng nghìn ASIC miner để đào bitcoin 24h một ngày. Công ty trả tiền điện bằng cách bán bitcoin đào được, tạo ra một khoảng thu nhập từ phần lợi nhuận có được.

### Mining giao dịch trong block

Những giao dịch mới được thêm vào network từ ví của người dùng và các ứng dụng khác tức thời. Vì chúng được nhìn thấy bởi bitcoin network node, chúng được thêm vào một tổ hợp tạm thời của những giao dịch chưa được xác minh bởi mỗi node. Khi mà miner xây dựng một block mới, họ thêm những giao dịch chưa được xác minh này tới một block mới và sau đó cố gắng giải quyết xác nhận cho block mới đó, với thuật toán mining (Proof-of-Work).  Quá trình mining được giải thích chi tiết trong phần [mining].

Giao dịch được thêm vào block mới, sắp xếp từ những giao dịch phí cao nhất và với vài thông tin khác. Mỗi miner sẽ bắt đầu quá trình đào một block mới của các giao dịch ngay khi nhận được block trước đó từ network, biết được rằng anh ta đã thua cuộc trong cuộc đua với block trước đó. Anh ta lập tức tạo ra một block mới, nạp đầy nó với các giao dịch và fingerprint của giao dịch trước đó, và bắt đầu tính toán Proof-of-Work cho block mới. Mỗi miner thêm vào một giao dịch đặc biệt vào trong block, cái mà sẽ trả cho phần thưởng tới địa chỉ bitcoin của anh ta (hiện tại 12.5 bitcoin được tạo mới) cộng thêm tổng phí giao dịch từ tất cả giao dịch tham gia vào trong block. Nếu anh ta tìm ra một lời giải chứng minh block là hợp lệ, anh ta "thắng" phần thưởng đó bởi vì block của anh được thêm vào trong blockchain toàn cầu và giao dịch phần thưởng (reward transaction) của anh trở lên có thể sử dụng được. Jing tham gia vào mining pool, đã thiết lập một phần mềm để tạo ra block mới mà gắn phần thưởng vào một tổ hợp địa chỉ riêng (pool address). Từ đó, một phần phần thưởng được chia sẻ tới Jing và những miner khác theo như phần trăm mà họ đóng góp trong phiên làm việc đó.

Giao dịch của Alice được chọn ra từ network và thêm vào pool của những giao dịch chưa được xác minh. Một khi được xác minh bởi phần mềm mining, nó được thêm vào trong một block mới, gọi là candidate block (block ứng cử), tạo bởi mining pool của Jing. Tất cả các miner tham gia vào mining pool đó ngay lập tức bắt đầu tính toán Proof-of-Work cho candidate block. Sau khoảng 5 phút kể từ khi giao dịch được chuyển đi từ ví của Alice, một trong những ASIC miner của Jing tìm ra một lời giải cho candidate block và thông báo cho network. Một khi các miner khác xác minh block thắng cuộc này, họ bắt đầu cuộc đua tạo ra một block mới.

Block chiến thắng của Jing tham gia vào blockchain với số hiệu block #277316, bao gồm 420 giao dịch, trong đó có giao dịch của Alice. Block có chứa giao dịch của Alice được tính là một "xác thực" cho giao dịch đó.

Tip
> Bạn có thể kiểm tra block có chứa [giao dịch của Alice](https://blockchain.info/block-height/277316)

Sau khoảng 19 phút sau đó, một block mới, #277317, được đào bởi một miner khác. Bởi vì block này được tạo ra ngay trên block #277316 chứa giao dịch của Alice, nó thêm vào nhiều tính toán hơn cho blockchain, do đó củng cố thêm độ tin cậy cho các giao dịch. Mỗi block được đào phía trên của block chứa giao dịch được tính là một sự xác minh thêm vào cho giao dịch của Alice. Vì block được đặt trên nhau, việc reverse giao dịch ngày càng khó hơn, do đó làm cho mạng lưới ngày càng đáng tin cậy.

Trong bảng giao dịch của Alice, gồm có block #277316, chúng ta có thể thấy được block #277316 chứa giao dịch của Alice. Bên dưới nó là 277,316 giao dịch (gồm cả block #0), kết nối mỗi trong số chúng tới blockchain, dẫn tới block số #0, được biết đến là block khởi nguồn. Qua thời gian, khi mà "độ dài" của các block tăng lên, thì độ phức tạp của tính toán của mỗi block cũng như toàn thể chuỗi cũng tăng lên. Những block được đào sau block chứa giao dịch của Alice vận hành như là sự đảm bảo thêm, vì chúng xếp tầng tạo nên nhiều tính toán hơn nữa cho cả chuỗi. Bằng sự thỏa thuận ngầm thì mỗi block với nhiều hơn 6 xác thực được cho là không thay đổi được, bởi vì nó sẽ cần một lượng tính toán khá lớn để làm mất hiệu lực và tính toán lại 6 block. Chúng ta sẽ xem xét quá trình minging và cách để xây dựng sự tin tưởng chi tiết hơn trong phần [mining].

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0209.png" style="width: 100%;" alt="Giao dịch của Alice bao gồm trong block #277316"/>
</div>

### Sử dụng một giao dịch

Bây giờ thì giao dịch của Alice đã được nhúng vào trong blockchain như là một phần của một block, nó là một phần của sổ cái bitcoin phân tán và hữu hình tới tất cả ứng dụng bitcoin. Mỗi một bitcoin client có thể xác thực giao dịch một cách độc lập. Full-node client có thể theo dấu vết nguồn của số tiền từ thời điểm bitcoin được tạo ra lần đầu trong một block, tăng dần theo giao dịch, cho đến khi đạt tới địa chỉ của Bob. Lightweight client có thể làm việc gọi là xác minh tối giản giao dịch thanh toán bằng cách xác nhận rằng giao dịch đó có trong blockchain và có vài block được đào sau nó, do đó cung cấp đảm bảo rằng miner đã chấp nhận nó hợp lệ.

Bob bây giờ có thể sử dụng output từ giao dịch này và các giao dịch khác. Ví dụ, Bob có thể trả cho nhân viên hoặc nhà cung cấp bằng việc chuyển **giá trị** từ thanh toán cốc cà phê của Alice tới những người chủ mới. Khả năng cao là phần mềm bitcoin của Bob sẽ tổng hợp nhiều thanh toán nhỏ để tạo ra một thanh toán lớn hơn, có thể là sẽ tập trung tất cả lợi nhuận bitcoin vào một giao dịch đơn lẻ. Điều này sẽ tổng hợp nhiều thanh toán vào một output duy nhất (và một địa chỉ duy nhất). Xem phần *Tổng hợp nguồn tài chính giao dịch* để biết về biểu đồ tổng hợp giao dịch.

Khi mà Bob dùng số tiền từ giao dịch của Alice và những khác hàng khác, anh ta đã làm việc mở rộng chuỗi giao dịch. Giả định rằng Bob trả phí cho Gopesh ở Bangalore cho trang web mới được thiết kế. Bây giờ chuỗi giao dịch sẽ giống như là giao dịch của Alice là một phần của chuỗi giao dịch từ Joe tới Gopesh.

<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0210.png" style="width: 100%;"/>
</div>


Trong chương này, chúng ta đã thấy được các giao dịch xây dựng lên chuỗi di chuyển **giá trị** từ chủ sở hữu này sang chủ sở hữu khác. Chúng ta cũng theo dõi được giao dịch của Alice, từ thời điểm nó được tạo ra trong ví của cô, trong bitcoin network và tới những miner lưu nó trong blockchain. Trong phần còn lại của cuốn sách, chúng ta sẽ nghiên cứu về công nghệ đằng sau ví bitcoin, địa chỉ, chữ ký, giao dịch và network, cuối cùng là mining.

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

# Chú thích

Sách dịch từ bản tiếng Anh của cuốn **Mastering Bitcoin**, bản open source trên [Github](https://github.com/bitcoinbook/bitcoinbook)
Bản tiếng Anh có thể mua trên [Amazon](https://www.amazon.com/Mastering-Bitcoin-Programming-Open-Blockchain/dp/1491954388) 

<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/cover.png" style="width: 320px;" />