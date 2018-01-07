---
title: "Làm chủ bitcoin - Chương 3"
tags: [mastering bitcoin, vietnamese, book, translate]
---
# Bitcoin Core: implement tham khảo chính thức

Bitcoin là một dự án open source và source code tồn tại dưới dạng giấy phép MIT, miễn phí để download và dùng dưới bất kỳ hình thức nào. Open source có ý nghĩ nhiều hơn là đơn thuần được miễn phí download. Nó cũng có nghĩa là bitcoin được phát triển bởi một cộng đồng mở bao gồm nhiều tình nguyện viên. Ban đầu thì cộng đồng đó chỉ bao gồm Nakamoto Satoshi. Nhưng cho đến thời điểm 2016, source code của bitcoin được đóng góp bởi hơn 400 người, một số làm việc toàn thời gian và số còn lại làm thêm bán thời gian. Bất kỳ ai cũng có thể đóng góp cho source code kể cả bạn!

Khi phát minh ra bitcoin, thực tế thì Nakamoto Satoshi đã hoàn thiện phần mềm ngay cả trước khi đăng bài paper. Satoshi làm vậy để chắc chắn rằng nó hoạt động trước khi viết bài. Implement đầu tiên đó, được biết đến là "Bitcoin" hay "Satoshi client", sau được cải tiến rất nhiều. Bản cải tiến này được biết đến là Bitcoin Core, để phân biệt với các bản implement tương thích khác. Bitcoin Core là bản tham khảo chính thức cho hệ thống, nghĩa là nó là bản tham khảo được chứng thực về việc hệ thống nên được implement như thế nào.  Bitcoin Core implement mọi thứ về bitcoin, bao gồm ứng dụng ví, giao dịch, và engine xác thực block và full network node trong mạng lưới bitcoin peer-to-peer.

Khuyến cáo
> Ngay cả khi Bitcoin Core bao gồm bản implement tham khảo ứng dụng ví, điều này không có nghĩa là chúng ta nên dùng như ứng dụng production cho người dùng hoặc các ứng dụng khác. Các nhà phát triển ứng dụng được khuyến cáo nên tạo ví dùng các tiêu chuẩn hiện đại như là BIP-39 hoặc BIP-32. BIP là từ viết tắt cho Bitcoin Improvement Proposal.

Kiến trúc của Bitcoin Core:
<div style="text-align: center;">
	<img src="https://raw.githubusercontent.com/bitcoinbook/bitcoinbook/second_edition/images/mbc2_0301.png" style="width: 100%;" alt="Kiến trúc của Bitcoin Core - Nguồn Eric Lombrozo"/>
</div>

## Môi trường phát triển bitcoin

Nếu là một nhà phát triển, bạn sẽ muốn thử thiết lập môi trường phát triển với tất cả các công cụ, thư viện và ứng dụng bổ trợ để viết ứng dụng bitcoin. Trong chương phần lớn về mặt kỹ thuật này, chúng ta sẽ tìm hiểu từng bước quá trình đó. Nếu đề tài trở lên quá khó (hoặc bạn không thực sự sẽ thiết lập môi trường phát triển) thì có thể bỏ qua xem chương kế tiếp, phần ít về kỹ thuật hơn.

## Biên dịch Bitcoin Core từ source code

Source code của Bitcoin Core có thể tải về bản nén ZIP hoặc clone source code từ repository trên GitHub. Từ trang GitHub của bitcoin, lựa chọn Download ZIP từ sidebar. Hoặc, dùng command line để tạo một bản copy local từ source code trên hệ thống của bạn.

Tip
> Trong nhiều ví dụ trong chương này, chúng ta sẽ dùng giao diện dòng lệnh command-line của hệ điều hành (còn được biết đến là "shell"), truy cập thông qua ứng dụng "terminal". Shell sẽ hiển thị dấu chờ lệnh (promt); bạn gõ một câu lệnh; và shell sẽ trả lại text và một ký tự chờ lệnh mới. Ký tự chờ lệnh có thể khác nhau tùy vào hệ thống, tuy nhiên trong những ví dụ sau đây sẽ được ký hiệu bằng ký tự **$**. Trong những ví dụ này, khi thấy text sau ký tự **$**, đừng gõ cả ký tự **$** mà chỉ gõ phần text theo sau nó, sau đó bấm *Enter* để thực thi câu lệnh. Trong những ví dụ này, dòng tiếp theo sau mỗi câu lệnh biểu diễn kết quả thực thi câu lệnh đó. Khi thấy một ký tự **$** mới, bạn biết rằng nó là một câu lệnh mới và bạn nên lặp lại quá trình như trên.

Trong ví dụ này, chúng ta dùng lệnh *git* để tạo một bản copy local ("clone") source code:

```
$ git clone https://github.com/bitcoin/bitcoin.git
Cloning into 'bitcoin'...
remote: Counting objects: 66193, done.
remote: Total 66193 (delta 0), reused 0 (delta 0), pack-reused 66193
Receiving objects: 100% (66193/66193), 63.39 MiB | 574.00 KiB/s, done.
Resolving deltas: 100% (48395/48395), done.
Checking connectivity... done.
$
```

Tip
> Git là một trong những ứng dụng phổ biến dùng để quản lý version phân tán, một phần không thể thiếu trong bộ toolkit cho nhà phát triển phần mềm. Bạn có thể phải cài đặt git command, hoặc giao diện đồ họa cho git cho hệ điều hành của bạn nếu nó chưa được cài.

Khi lệnh git clone hoàn tất, bạn sẽ có một bản copy trên local của source code trong thư mục *bitcoin*. Di chuyển vào thư mục đó bằng cách gõ **cd bitcoin**:

```
$ cd bitcoin
```

### Lựa chọn một bản Release cho Bitcoin Core

Mặc định thì bản copy local sẽ đồng bộ với code gần đây nhất, thường có thể là bản chưa ổn định hoặc là bản beta của bitcoin. Trước khi thực hiện compile code, lựa chọn một bản cụ thể bằng cách kiểu tra tag release. Việc này sẽ đồng bộ bản copy local với một bản snapshot của repository source code bằng từ khóa tag. Tag thường được nhà phát triển dùng để đánh dấu các bản release của source code bằng một con số version cụ thể. Đầu tiên, kiểm tra các tag hiện hữu, bằng cách dùng câu lệnh git tag:

    $ git tag
    v0.1.5
    v0.1.6test1
    v0.10.0
    ...
    v0.11.2
    v0.11.2rc1
    v0.12.0rc1
    v0.12.0rc2
    ...

Danh sách tag thể hiện những version đã được release của bitcoin. Theo quy ước, các bản release mà mục đích là cho việc test, sẽ có đuôi "rc". Các bản release ổn định có thể chạy trên môi trường production thì không có hậu tố như vậy. Từ danh sách trên, lựa chọn bản release với version cao nhất, hiện thời tại thời điểm viết sách là *v0.11.2*. Để đồng bộ code local với version này, dùng lệnh git:

    $ git checkout v0.11.2
    HEAD is now at 7e27892... Merge pull request #6975

Bạn có thể xác nhận version có đúng đã được "checked out" hay không bằng việc dùng lệnh git status:

    $ git status
    HEAD detached at v0.11.2
    nothing to commit, working directory clean

### Cấu hình Bitcoin Core Build

Source code bao gồm cả tài liệu, chúng ta có thể tìm thấy chúng trong một số file. Xem phần tài liệu chính tại file *README.md* tại thư mục bitcoin bằng cách gõ **more README.md** và dùng space key để  di chuyển tới trang kế tiếp. Trong chương này, chúng ta sẽ xây dựng command-line bitcoin client, còn được biết đến với tên gọi *bitcoind* trên Linux. Xem hướng dẫn để compile bitcoind command-line client bằng cách gõ **more doc/build-unix.md**. Hướng dẫn cho MacOS và Windows có thể được tìm thấy ở thư mục *doc*, với tên file lần lượt là *build-osx.md* hoặc *build-windows.md*.

Trước khi build, cần xem kỹ phần điều kiện cần, thứ là một phần của tài liệu build. Có những thư viện phải có trong hệ điều hành của bạn trước khi bắt đầu compile bitcoin. Nếu như thiếu những điều kiện tiên quyết này thì việc build sẽ thất bại với lỗi xảy ra. Nếu điều này xảy ra, bạn có thể cài những thư viện cần này trước, sau đó thử build lại từ bước bị lỗi. Giả định rằng các thư viện cần đã được cài, bạn có thể bắt đầu quá trình build bằng cách sinh ra tập các script build dùng script *autogen.sh*.

Note
> Quá trình build Bitcoin Core thay đổi từ version 0.9, dùng *autogen/configure/make*. Những version cũ hơn dùng một file *Makefile* đơn giản và hoạt động hơi khác với ví dụ sau đây một chút. Hãy làm theo hướng dẫn của version mà bạn muốn compile. *autogen/configure/make* có khả năng cao sẽ là cách build cho các version trong tương lai và được dùng cho ví dụ sau đây.

```
$ ./autogen.sh
...
glibtoolize: copying file 'build-aux/m4/libtool.m4'
glibtoolize: copying file 'build-aux/m4/ltoptions.m4'
glibtoolize: copying file 'build-aux/m4/ltsugar.m4'
glibtoolize: copying file 'build-aux/m4/ltversion.m4'
...
configure.ac:10: installing 'build-aux/compile'
configure.ac:5: installing 'build-aux/config.guess'
configure.ac:5: installing 'build-aux/config.sub'
configure.ac:9: installing 'build-aux/install-sh'
configure.ac:9: installing 'build-aux/missing'
Makefile.am: installing 'build-aux/depcomp'
...
```

*autogen.sh* script tạo ra tự động các script thiết lập mà sẽ xem xét hệ thống trên local để tìm ra thiết lập đúng đắn và chắc chắn rằng máy local có đủ thư viện cần thiết cho việc compile code. Phần quan trọng nhất là script thiết lập giúp chúng ta có một số lựa chọn để tùy chỉnh quá trình build. Gõ **./configure --help** để xem những tùy chọn này:

    $ ./configure --help
    `configure' configures Bitcoin Core 0.11.2 to adapt to many kinds of systems.

    Usage: ./configure [OPTION]... [VAR=VALUE]...

    ...
    Optional Features:
    --disable-option-checking  ignore unrecognized --enable/--with options
    --disable-FEATURE       do not include FEATURE (same as --enable-FEATURE=no)
    --enable-FEATURE[=ARG]  include FEATURE [ARG=yes]

    --enable-wallet         enable wallet (default is yes)

    --with-gui[=no|qt4|qt5|auto]
    ...

Script thiết lập cho phép bạn kích hoạt hoặc vô hiệu hóa những tính năng nhất định của *bitcoind* bằng cách thêm cờ --enable-FEATURE và --disable-FEATURE. Ở đây *FEATURE* được thay thế bằng tên tính năng, được liệt kê tại phần help output. Trong chương này, chúng ta sẽ build *bitcoind* client với tất cả tính năng mặc định. Chúng ta sẽ không dùng cờ thiết lập, tuy nhiên bạn nên xem qua chúng để biết được những tùy chọn tính năng nào có thể có cho client. Nếu bạn cần thiết lập mang tính học thuật, hoặc bị hạn chế bởi phòng lab máy tính, bạn có thể phải cài đặt ứng dụng tại thư mục home (e.g., dùng cờ --prefix=$HOME).

Sau đây là một số tùy chọn hữu ích ghi đè tập tính mặc định của script thiết lập:

**--prefix=$HOME**
Cờ này ghi đè thư mục cài mặc định (là /usr/local/). Dùng *$HOME* để cài đặt vào thư mục home, hoặc một đường dẫn khác.

**--disable-wallet**
Cờ này được dùng để vô hiệu hóa tham chiếu đến implement của ví.

**--with-incompatible-bdb**
Nếu bạn build ví, cờ này cho phép sử dụng bản không tương thích của thư viện Berkeley DB.

**--with-gui=no**
Không build giao diệp đồ họa, cái mà cần có thư viện Qt. Với cờ này thì chúng ta chỉ build server và command-line cho bitcoin.

Tiếp theo, chạy script thiết lập để tự động tìm ra những thư viện cần thiết, và tạo một bản script build đã được tùy chỉnh cho hệ thống của bạn:

    $ ./configure
    checking build system type... x86_64-unknown-linux-gnu
    checking host system type... x86_64-unknown-linux-gnu
    checking for a BSD-compatible install... /usr/bin/install -c
    checking whether build environment is sane... yes
    checking for a thread-safe mkdir -p... /bin/mkdir -p
    checking for gawk... gawk
    checking whether make sets $(MAKE)... yes
    ...
    [many pages of configuration tests follow]
    ...
    $

Nếu mọi việc suôn sẻ, lệnh *configure* sẽ kết thúc bằng việc tạo ra những script build đã tùy biến cho phép chúng ta compile *bitcoind*. Nếu như có bất kỳ thư viện hoặc lỗi nào, lệnh *configure* sẽ kết thúc với một lỗi nào đó thay vì tạo ra build script. Nếu xảy ra lỗi, thường thì là do bị thiếu thư viện hoặc do thư viện không tương thích. Xem lại tài liệu build trong trường hợp đó và chắc chắn rằng bạn đã cài đầy đủ các điều kiện cần. Sau đó chạy *configure* thêm lần nữa và xem thử xem lỗi đã được sửa hay chưa.

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

### Cài đặt Bitcoin Core Executables

Tiếp theo, bạn sẽ compile source code, là quá trình mất khoảng 1 tiếng để hoàn tất, phụ thuộc vào tốc độ của CPU và memory. Trong quá trình compile này, bạn sẽ thấy được output sau mỗi vài giây hoặc sau vài phút, hoặc thấy một lỗi nào đó nếu có gì đó không đúng. Nếu xảy ra lỗi, quá trình compile sẽ bị gián đoạn, và nó có thể chạy lại bất kỳ lúc nào bằng cách gõ *make* lần nữa. Gõ lệnh **make** để bắt đầu compile ứng dụng chạy:

    ls -
    $ make
    Making all in src
    CXX      crypto/libbitcoinconsensus_la-hmac_sha512.lo
    CXX      crypto/libbitcoinconsensus_la-ripemd160.lo
    CXX      crypto/libbitcoinconsensus_la-sha1.lo
    CXX      crypto/libbitcoinconsensus_la-sha256.lo
    CXX      crypto/libbitcoinconsensus_la-sha512.lo
    CXX      libbitcoinconsensus_la-hash.lo
    CXX      primitives/libbitcoinconsensus_la-transaction.lo
    CXX      libbitcoinconsensus_la-pubkey.lo
    CXX      script/libbitcoinconsensus_la-bitcoinconsensus.lo
    CXX      script/libbitcoinconsensus_la-interpreter.lo

    [... many more compilation messages follow ...]

    $

Nếu mọi thứ diễn ra tốt đẹp, Bitcoin Core đã được biên dịch. Bước cuốn cùng là việc cài đặt các chương trình chạy được vào hệ thống dùng lệnh `sudo make install`. Có thể bạn sẽ được gợi ý nhập mật khẩu, vì câu lệnh này cần quyền admin:

    $ sudo make install
    Password:
    Making install in src
    ../build-aux/install-sh -c -d '/usr/local/lib'
    libtool: install: /usr/bin/install -c bitcoind /usr/local/bin/bitcoind
    libtool: install: /usr/bin/install -c bitcoin-cli /usr/local/bin/bitcoin-cli
    libtool: install: /usr/bin/install -c bitcoin-tx /usr/local/bin/bitcoin-tx
    ...
    $

Thư mục mặc định cài đặt *bitcoind* là `/usr/local/bin`. Bạn có thể xác nhận lại việc Bitcoin Core đã được cài đặt chính xác hay chưa bằng việc hỏi lại hệ thống đường dẫn của file chạy, như sau đây:

    $ which bitcoind
    /usr/local/bin/bitcoind

    $ which bitcoin-cli
    /usr/local/bin/bitcoin-cli

### Chạy Bitcoin Core Node

Mạng lưới peer-to-peer của bitcoin gồm có các "node", chạy bởi các tình nguyện viên và một số người làm business build ứng dụng bitcoin. Những node bitcoin đó đều nhìn được trực tiếp và có thẩm quyền đối với bitcoin blockchain, gồm có bản copy local cho mọi giao dịch, được công nhận một cách độc lập trên hệ thống của họ. Bằng việc chạy một node, bạn không phải dựa vào bất kỳ bên thứ ba nào để xác nhận giao dịch. Hơn nữa, bằng việc chạy bitcoin node, bạn đã đóng góp vào bitcoin network bằng cách làm cho nó thêm phần chắc chắn hơn.

Tuy nhiên việc chạy một node cần một hệ thống kết nối thường trực với đủ tài nguyên để xử lý tất cả các giao dịch. Tùy thuộc vào việc bạn có tạo index cho toàn bộ giao dịch và giữ toàn bộ cản copy của blockchain hay không, bạn có thể cần rất nhiều không gian ổ đĩa và RAM. Tại thời điểm cuối năm 2016, một node với full-index cần 2GB RAM và 125 GB không gian ổ đĩa. Các node của bitcoin cũng cần phải truyền và nhận giao dịch bitcoin và block, do đó tiêu thụ một lượng đường truyền internet. Nếu kết nối internet của bạn bị giới hạn, có băng thông thấp, hoặc bị tính tiền theo lưu lượng sử dụng, bạn không nên chạy bitcoin node trên máy của mình hoặc phải chạy cách có thể tiết kiệm băng thông (xem phần hướng dẫn về thiết lập hệ thống tài nguyên).

Tip
> Bitcoin Core mặc định giữ bộ copy của toàn bộ blockchain, với tất cả các giao dịch đã từng diễn ra trên mạng lưới bitcoin từ lúc bắt đầu là 2009. Bộ dữ liệu này khoảng vài chục gigabytes và được tải về tăng dần sau vài ngày hoặc vài tuần, tùy vào tốc độ CPU và tốc độ đường truyền. Bitcoin Core không thể xử lý giao dịch hoặc cập nhật tiền tài khoản cho đến khi bộ dữ liệu blockchain đã được tải về hoàn toàn. Hãy chắc chắn rằng bạn có đủ không gian ổ đĩa, băng thông và thời gian để kết thúc quá trình đồng bộ đầu tiên. Bạn có thể thiếp lập Bitcoin Core để giảm kích thước blockchain bằng việc loại bỏ những block cũ (xem ví dụ về thiết lập hệ thống tài nguyên), tuy nhiên nó vẫn sẽ phải tải về toàn bộ bộ dữ liệu trước khi loại bỏ dữ liệu đó.

Cho dù có những yêu cầu về tài nguyên như vậy, hàng nghìn người tình nguyện vẫn chạy bitcoin node. Thậm chí một số còn chạy trên hệ thống đơn giản như là Raspberry (máy tính kích cỡ nhỏ giá khoảng $35 USD). Một số người tình nguyện còn chạy bitcoin node trên server cho thuê, thường là các loại máy Linux. Instance của Virtual Private Server (VPS) hoặc Cloud Computing Server có thể được dùng làm bitcoin node. Những server như vậy có thể được thuê với $25 cho đến $50 USD mỗi tháng từ nhiều nhà cung cấp.

Tại sao bạn lại muốn chạy một node? Sau đây là một số lý do thông thường:

* Nếu bạn đang phát triển ứng dụng bitcoin và cần dựa vào bitcoin node để truy cập đến API của mạng lưới và blockchain.

* Nếu bạn đang xây dựng ứng dụng mà cần xác nhận giao dịch theo như luật về thỏa thuận của bitcoin. Thường sẽ là những công ty bitcoin chạy nhiều node.

* Nếu bạn muốn giúp đỡ bitcoin. Chạy node củng cố sự chắc chắn cho mạng lưới và giúp phục vụ nhiều ví, nhiều người dùng và nhiều giao dịch hơn.

* Nếu bạn không muốn dựa vào một bên thứ 3 để xác thực giao dịch của bạn.

Nếu bạn đọc cuốn sách này và có hứng thú với việc phát triển ứng dụng bitcoin, bạn nên chạy node cho của riêng mình.

## Chạy Bitcoin Core lần đầu tiên

Khi bạn chạy *bitcoind* lần đầu tiên, nó sẽ nhắc nhở bạn tạo một file cấu hình với một mật khẩu đủ mạnh cho giao diện JSON-RPC. Mật khẩu này dùng cho việc quản lý truy cập đến API của Bitcoin Core.

Chạy *bitcoind* bằng cách gõ **bitcoind** trên terminal:

    $ bitcoind
    Error: To use the "-server" option, you must set a rpcpassword in the configuration file:
    /home/ubuntu/.bitcoin/bitcoin.conf
    It is recommended you use the following random password:
    rpcuser=bitcoinrpc
    rpcpassword=2XA4DuKNCbtZXsBQRRNDEwEY2nM6M4H9Tx5dFjoAVVbK
    (you do not need to remember this password)
    The username and password MUST NOT be the same.
    If the file does not exist, create it with owner-readable-only file permissions.
    It is also recommended to set alertnotify so you are notified of problems;
    for example: alertnotify=echo %s | mail -s "Bitcoin Alert" admin@foo.com


Như bạn thấy được, tại lần đầu chạy *bitcoind*, nó sẽ bảo rằng bạn cần build file cấu hình, với ít nhất một entry *rpcuser* và *rpcpassword*. Thêm vào đó, nó gợi ý rằng bạn nên thiết lập cơ chế báo động. Trong phần tiếp theo, chúng ta sẽ tìm hiểu các tùy chọn này và thiết lập file configuration.

### Thiết lập Bitcoin Core Node

Thay đổi file configuration với editor của bạn và thiết lập các tham số, thay password với mật khẩu đủ mạnh. Chú ý không dùng mật khẩu giới thiệu trong sách này. Tạo một file trong thư mục *.bitcoin* (bên trong thư mục home) và lấy tên là *./bitcoin/bitcoin.conf* đồng thời cung cấp username và password:

    rpcuser=bitcoinrpc
    rpcpassword=CHANGE_THIS

Ngoài tùy chọn về *rpcuser* và *rpcpassword*, Bitcoin Core cung cấp nhiều hơn 100 tùy chỉnh cấu hình khác dùng để thay đổi cách vận hành của network node, storage của blockchain, và các khía cạnh khác nữa. Để thấy toàn bộ danh sách này, chạy lệnh `bitcoind --help`:


    bitcoind --help
    Bitcoin Core Daemon version v0.11.2

    Usage:
    bitcoind [options]                     Start Bitcoin Core Daemon

    Options:

    -?
        This help message

    -alerts
        Receive and display P2P network alerts (default: 1)

    -alertnotify=<cmd>
        Execute command when a relevant alert is received or we see a really
        long fork (%s in cmd is replaced by message)
    ...
    [many more options]
    ...

    -rpcsslciphers=<ciphers>
        Acceptable ciphers (default:
        TLSv1.2+HIGH:TLSv1+HIGH:!SSLv2:!aNULL:!eNULL:!3DES:@STRENGTH)


Sau đây là một số tùy chọn quan trọng mà bạn có thể thiết lập qua configuration file, hoặc dùng tham số của *bitcoind* qua command-line:

**alertnotify**
Chạy một lệnh đặc biệt để gửi alert khẩn cấp tới chủ sở hữu của node, thường là bằng email.

**conf**
Một ví trí thay thế cho configuration file. Chỉ tương thích với tham số của *bitcoind* command-line bởi nó không thể bên trong chính configuration file.

**datadir**
Thư mục và filesystem để đặt dữ liệu blockchain. Mặc định thì là *.bitcoin* dưới thư mục *home*. Chắc chắn rằng thư mục này có không gian khoảng trống vài gigabytes.

**prune**
Giảm yêu cầu về lưu trữ ổ cứng tới con số megabytes này, bằng việc xóa bỏ những block cũ. Dùng tùy chọn này trên *resource-constrained node*, là cái không chứa được toàn bộ blockchain.

**txindex**
Quản lý index cho giao dịch. Điều này có nghĩa toàn bộ copy của blockchain cho phép bạn lập trình nhận bất kỳ giao dịch nào bằng ID.

**maxconnections**
Thiết lập tổng số node từ đó chấp nhận kết nối. Giảm con số này đồng nghĩa với việc giảm việc tiêu thụ băng thông đường truyền. Dùng nó khi bạn có giới hạn dữ liệu hoặc đường truyền trả theo gigabyte.

**maxmempool**
Giới hạn memory pool của giao dịch tới con số megabytes này. Dùng tùy chọn này để giảm độ dùng memory của node.

**maxreceivebuffer/maxsendbuffer**
Giới hạn bộ đệm memory cho mỗi kết nối tới con số này nhân với 1000 bytes. Dùng cho *memory-constrained node*.

**minrelaytxfee**
Thiết lập phí thấp nhất cho giao dịch mà bạn sẽ chuyển tiếp. Phí nhỏ hơn con số này sẽ được coi như bằng 0. Dùng tùy chọn này trên *memory-constrained node* để giảm kích thước của pool giao dịch *in-memory*.


Index cơ sở dữ liệu giao dịch và tùy chọn txindex

Mặc định thì Bitcoin Core build cơ sở dữ liệu chỉ chứa giao dịch liên quan tới ví của người dùng. Nếu như bạn muốn có khả năng truy cập bất kỳ giao dịch nào với lệnh ví dụ như `getrawtransaction` (xem phần **Khám phá và Decode giao dịch**), bạn sẽ cần phải cấu hình Bitcoin Core để build toàn bộ index cho các giao dịch, điều này có thể làm được với tùy chọn *txindex*. Thiết lập `txindex=1` trong file cấu hình Bitcoin Core. Nếu bạn không thiết lập tùy chọn này lúc đầu nhưng muốn thay đổi sau đó, bạn cần khởi động lại bitcoind với tùy chọn -reindex và đợi cho nó build index.


**Ví dụ configuration của node full-index** cho chúng ta biết các tùy chọn có thể kết hợp với nhau như thế nào, với các node được index hoàn toàn, chạy như là API phía backend cho ứng dụng bitcoin.

Ví dụ 1. Ví dụ configuration của node full-index

    alertnotify=myemailscript.sh "Alert: %s"
    datadir=/lotsofspace/bitcoin
    txindex=1
    rpcuser=bitcoinrpc
    rpcpassword=CHANGE_THIS

Ví dụ về hệ thống resource-constrain chỉ ra một node resource-constrain chạy trên một server bé hơn.

Ví dụ 2. Ví dụ về hệ thống resource-constrain

    alertnotify=myemailscript.sh "Alert: %s"
    maxconnections=15
    prune=5000
    minrelaytxfee=0.0001
    maxmempool=200
    maxreceivebuffer=2500
    maxsendbuffer=500
    rpcuser=bitcoinrpc
    rpcpassword=CHANGE_THIS

Khi mà bạn đã tùy biến configuration file và thiết lập tùy biến thích hợp nhất cho nhu cầu của mình, bạn có thể thử bitcoind với những thiết lập này. Chạy Bitcoin Core với tùy chọn *printtoconsole* để chạy foreground với output ra console:

    $ bitcoind -printtoconsole

    Bitcoin version v0.11.20.0
    Using OpenSSL version OpenSSL 1.0.2e 3 Dec 2015
    Startup time: 2015-01-02 19:56:17
    Using data directory /tmp/bitcoin
    Using config file /tmp/bitcoin/bitcoin.conf
    Using at most 125 connections (275 file descriptors available)
    Using 2 threads for script verification
    scheduler thread start
    HTTP: creating work queue of depth 16
    No rpcpassword set - using random cookie authentication
    Generated RPC authentication cookie /tmp/bitcoin/.cookie
    HTTP: starting 4 worker threads
    Bound to [::]:8333
    Bound to 0.0.0.0:8333
    Cache configuration:
    * Using 2.0MiB for block index database
    * Using 32.5MiB for chain state database
    * Using 65.5MiB for in-memory UTXO set
    init message: Loading block index...
    Opening LevelDB in /tmp/bitcoin/blocks/index
    Opened LevelDB successfully

    [... more startup messages ...]


Bạn có thể bấm Ctrl-C để làm gián đoạn tiến trình một khi bạn đã xác nhận được nó nhận đúng thiết lập và chạy như mong đợi.

Để chạy Bitcoin Core như tiến trình background, bắt đầu với lựa chọn daemon, `bitcoind -daemon`.

Để theo dõi tiến trình và có trạng thái tức thời của bitcoin node, dùng command `bitcoin-cli getinfo`:

    $ bitcoin-cli getinfo
    {
        "version" : 110200,
        "protocolversion" : 70002,
        "blocks" : 396328,
        "timeoffset" : 0,
        "connections" : 15,
        "proxy" : "",
        "difficulty" : 120033340651.23696899,
        "testnet" : false,
        "relayfee" : 0.00010000,
        "errors" : ""
    }

Câu lệnh ở trên cho biết node chạy Bitcoin Core version *0.11.2*, với độ dài blockchain là 396328 block và có 15 kết nối active.

Một khi bạn đã cảm thấy ổn với thiết lập mình đã lựa chọn, bạn nên thêm bitcoin vào script khi khởi động máy, để nó có thể chạy liên tục và restart khi hệ điều hành restart. Bạn có thể tìm được ví dụ về các script startup cho nhiều loại hệ điều hành khác nhau trong thư mục `contrib/init` và một file *README.md* chỉ ra hệ thống nào dùng script nào.

## Bitcoin Core Application Programming Interface (API)

Bitcoin Core client implement giao diện JSON-RPC, có thể truy cập dùng helper của lệnh console `bitcoin-cli`. Câu lệnh cho phép chúng ta thử trực tiếp những tính năng có thể dùng để lập trình thông qua API. Để bắt đầu, chạy lệnh `help` để thấy được những lệnh gì có thể dùng được cho bitcoin RPC:

    $ bitcoin-cli help
    addmultisigaddress nrequired ["key",...] ( "account" )
    addnode "node" "add|remove|onetry"
    backupwallet "destination"
    createmultisig nrequired ["key",...]
    createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,...}
    decoderawtransaction "hexstring"
    ...
    ...
    verifymessage "bitcoinaddress" "signature" "message"
    walletlock
    walletpassphrase "passphrase" timeout
    walletpassphrasechange "oldpassphrase" "newpassphrase"

Mỗi câu lệnh ở trên có một số tham số. Để có thêm thông tin, thêm vào tên của command sau từ khóa `help`. Ví dụ, để tìm thông tin về command `getblockhash` RPC:

    $ bitcoin-cli help getblockhash
    getblockhash index

    Returns hash of block in best-block-chain at index provided.

    Arguments:
    1. index         (numeric, required) The block index

    Result:
    "hash"         (string) The block hash

    Examples:
    > bitcoin-cli getblockhash 1000
    > curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockhash", "params": [1000] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/

Tại phần cuối của thông tin help, bạn có thể thấy 2 ví dụ về command RPC, dùng `bitcoin-cli helper` hoặc dùng `HTTP client curl`. Những ví dụ này biểu diễn cho chúng ta biết command có thể được gọi như thế nào. Copy ví dụ thứ nhất và xem kết quả:

    $ bitcoin-cli getblockhash 1000
    00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09

Kết quả trả về là một block hash, sẽ được trình bày kỹ hơn trong các chương kế tiếp. Hiện tại thì lệnh này sẽ trả về cùng kết quả trên máy của bạn, biểu diễn rằng Bitcoin Core node đang chạy, chấp nhận command và có thông tin về block 1000 để trả về.

Trong phần tiếp theo chúng ta sẽ demo một số lệnh RPC hữu ích và kiểm tra output của chúng.

### Kiểm tra thông tin Status của Bitcoin Core Client

Command: getinfo

Lệnh `getinfo` hiển thị thông tin cơ bản về trạng thái của bitcoin network node, ví, và dữ liệu blockchain. Dùng `bitcoin-cli` để chạy lệnh này:

    $ bitcoin-cli getinfo
    {
        "version" : 110200,
        "protocolversion" : 70002,
        "blocks" : 396367,
        "timeoffset" : 0,
        "connections" : 15,
        "proxy" : "",
        "difficulty" : 120033340651.23696899,
        "testnet" : false,
        "relayfee" : 0.00010000,
        "errors" : ""
    }

Dữ liệu trả về dưới dạng JavaScript Object Notation (JSON), là dạng dễ dàng dùng cho lập trình nhưng đồng thời cũng thân thiện với con người. Trong dữ liệu này chúng ta thấy được số version của ứng dụng bitcoin client (110200) và bitcoin protocol (70002). Chúng ta thấy được độ dài block hiện tại, bao nhiêu block được biết bởi client này (396367). Chúng ta cũng thấy một số thông tin thống kê về bitcoin network và thông tin liên quan client.

Tip
> Để bitcoind có thể lấy được độ dài của blockchain hiện tại thì nó có thể mất thời gian nhiều hơn một ngày vì nó cần phải tải các block từ những client khác. Bạn có thể kiểm tra tiến trình này dùng lệnh `getinfo` để biết được số block đã được tìm ra.

### Khám phá và Decode giao dịch

Commands: getrawtransaction, decoderawtransaction

Trong phần trước, Alice mua một cốc cà phê từ quán của Bob. Giao dịch của cô được lưu vào blockchain với giao dịch ID (txid) `0627052b6f28912f2703066a912ea577f2ce4da4caa5a5fbd8a57286c345c2f2`. Hãy cùng thử dùng API để xác nhận giao dịch này:

    $ bitcoin-cli getrawtransaction 0627052b6f28912f2703066a912ea577f2ce4da4caa5a↵
    5fbd8a57286c345c2f2

    0100000001186f9f998a5aa6f048e51dd8419a14d8a0f1a8a2836dd734d2804fe65fa35779000↵
    000008b483045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1deccbb6498c75c4↵
    ae24cb02204b9f039ff08df09cbe9f6addac960298cad530a863ea8f53982c09db8f6e3813014↵
    10484ecc0d46f1918b30928fa0e4ed99f16a0fb4fde0735e7ade8416ab9fe423cc54123363767↵
    89d172787ec3457eee41c04f4938de5cc17b4a10fa336a8d752adfffffffff0260e3160000000↵
    0001976a914ab68025513c3dbd2f7b92a94e0581f5d50f654e788acd0ef8000000000001976a9↵
    147f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a888ac00000000

Tip
> Một ID giao dịch không được công nhận cho đến khi giao dịch đó được xác minh. Hash của giao dịch nếu bị thiếu trong blockchain cũng không có nghĩa là giao dịch đó đã không được xử lý. Cái này được biết đến là "tính dễ rèn của giao dịch", bởi vì các hash của giao dịch có thể được thay đổi trước đó để xác nhận trong một block. Sau khi đã được xác nhận, txid không thay đổi được (immutable) và trở lên được công nhận.

Lệnh `getrawtransaction` trả về một giao dịch dưới dạng số hệ cơ số 16. Để decode chuỗi này, chúng ta dùng lệnh `decoderawtransaction`, gửi dữ liệu hexa làm tham số. Bạn có thể copy giá trị hex trả về từ lệnh `getrawtransaction` và paste nó dùng làm tham số cho lệnh `decoderawtransaction`:

    $ bitcoin-cli decoderawtransaction 0100000001186f9f998a5aa6f048e51dd8419a14d8↵
    a0f1a8a2836dd734d2804fe65fa35779000000008b483045022100884d142d86652a3f47ba474↵
    6ec719bbfbd040a570b1deccbb6498c75c4ae24cb02204b9f039ff08df09cbe9f6addac960298↵
    cad530a863ea8f53982c09db8f6e381301410484ecc0d46f1918b30928fa0e4ed99f16a0fb4fd↵
    e0735e7ade8416ab9fe423cc5412336376789d172787ec3457eee41c04f4938de5cc17b4a10fa↵
    336a8d752adfffffffff0260e31600000000001976a914ab68025513c3dbd2f7b92a94e0581f5↵
    d50f654e788acd0ef8000000000001976a9147f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a8↵
    88ac00000000

    {
    "txid": "0627052b6f28912f2703066a912ea577f2ce4da4caa5a5fbd8a57286c345c2f2",
    "size": 258,
    "version": 1,
    "locktime": 0,
    "vin": [
        {
        "txid": "7957a35fe64f80d234d76d83a2...8149a41d81de548f0a65a8a999f6f18",
        "vout": 0,
        "scriptSig": {
            "asm":"3045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1decc...",
            "hex":"483045022100884d142d86652a3f47ba4746ec719bbfbd040a570b1de..."
        },
        "sequence": 4294967295
        }
    ],
    "vout": [
        {
        "value": 0.01500000,
        "n": 0,
        "scriptPubKey": {
            "asm": "OP_DUP OP_HASH160 ab68...5f654e7 OP_EQUALVERIFY OP_CHECKSIG",
            "hex": "76a914ab68025513c3dbd2f7b92a94e0581f5d50f654e788ac",
            "reqSigs": 1,
            "type": "pubkeyhash",
            "addresses": [
            "1GdK9UzpHBzqzX2A9JFP3Di4weBwqgmoQA"
            ]
        }
        },
        {
        "value": 0.08450000,
        "n": 1,
        "scriptPubKey": {
            "asm": "OP_DUP OP_HASH160 7f9b1a...025a8 OP_EQUALVERIFY OP_CHECKSIG",
            "hex": "76a9147f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a888ac",
            "reqSigs": 1,
            "type": "pubkeyhash",
            "addresses": [
            "1Cdid9KFAaatwczBwBttQcwXYCpvK8h7FK"
            ]
        }
        }
    ]
    }

Decode của giao dịch hiển thị tất cả các thành phần của giao dịch, bao gồm cả input và output. Trong trường hợp này, chúng ta thấy được rằng giao dịch được tạo ra bởi địa chỉ mới với 50 millibits dùng 1 input và tạo ra 2 output. Input của giao dịch này là output từ giao dịch trước đó (biển diễn với vin txid bắt đầu với 7957a35fe). Hai output lần lượt là 50 millibit credit và output tiền thừa trả về cho người gửi.

Chúng ta có thể tìm hiển blockchain bằng cách xem xét giao dịch trước đó mà được tham chiếu bởi txid trong phần giao sịch dùng lệnh (như là `getrawtransaction`). Đi từ giao dịch đến giao dịch chúng ta có thể theo dõi được chuỗi các giao dịch trở về trước khi mà coin được truyền từ người sở hữu này đến người sở hữu khác.

### Tìm hiểu block

Commands: getblock, getblockhash

Tìm hiểu block cũng giống như việc tìm hiểu giao dịch. Tuy nhiên, block được tham chiếu dựa vào chiều dài của block hoặc bằng block hash. Đầu tiên chúng ta sẽ tìm một block dùng độ dài của nó. Trong phần mua cà phê, chúng ta thấy rằng giao dịch của Alice được thực hiện trong block 277316.

Chúng ta dùng lệnh `getblockhash`, lấy chiều dài block làm tham số và trả về block hash của block đó:

    $ bitcoin-cli getblockhash 277316
    0000000000000001b6b9a13b095e96db41c4a928b97ef2d944a9b31b2cc7bdc4

Bây giờ chúng đã biết block chứa giao dịch của Alice, chúng ta có thể query block đó. Dùng lệnh `getblock` với block hash là tham số:

    $ bitcoin-cli getblock 0000000000000001b6b9a13b095e96db41c4a928b97ef2d944a9b3↵
    1b2cc7bdc4
    {
    "hash": "0000000000000001b6b9a13b095e96db41c4a928b97ef2d944a9b31b2cc7bdc4",
    "confirmations": 37371,
    "size": 218629,
    "height": 277316,
    "version": 2,
    "merkleroot": "c91c008c26e50763e9f548bb8b2fc323735f73577effbc55502c51eb4cc7cf2e",
    "tx": [
        "d5ada064c6417ca25c4308bd158c34b77e1c0eca2a73cda16c737e7424afba2f",
        "b268b45c59b39d759614757718b9918caf0ba9d97c56f3b91956ff877c503fbe",
        "04905ff987ddd4cfe603b03cfb7ca50ee81d89d1f8f5f265c38f763eea4a21fd",
        "32467aab5d04f51940075055c2f20bbd1195727c961431bf0aff8443f9710f81",
        "561c5216944e21fa29dd12aaa1a45e3397f9c0d888359cb05e1f79fe73da37bd",
    [... hundreds of transactions ...]
        "78b300b2a1d2d9449b58db7bc71c3884d6e0579617e0da4991b9734cef7ab23a",
        "6c87130ec283ab4c2c493b190c20de4b28ff3caf72d16ffa1ce3e96f2069aca9",
        "6f423dbc3636ef193fd8898dfdf7621dcade1bbe509e963ffbff91f696d81a62",
        "802ba8b2adabc5796a9471f25b02ae6aeee2439c679a5c33c4bbcee97e081196",
        "eaaf6a048588d9ad4d1c092539bd571dd8af30635c152a3b0e8b611e67d1a1af",
        "e67abc6bd5e2cac169821afc51b207127f42b92a841e976f9b752157879ba8bd",
        "d38985a6a1bfd35037cb7776b2dc86797abbb7a06630f5d03df2785d50d5a2ac",
        "45ea0a3f6016d2bb90ab92c34a7aac9767671a8a84b9bcce6c019e60197c134b",
        "c098445d748ced5f178ef2ff96f2758cbec9eb32cb0fc65db313bcac1d3bc98f"
    ],
    "time": 1388185914,
    "mediantime": 1388183675,
    "nonce": 924591752,
    "bits": "1903a30c",
    "difficulty": 1180923195.258026,
    "chainwork": "000000000000000000000000000000000000000000000934695e92aaf53afa1a",
    "previousblockhash": "0000000000000002a7bbd25a417c0374cc55261021e8a9ca74442b01284f0569",
    "nextblockhash": "000000000000000010236c269dd6ed714dd5db39d36b33959079d78dfd431ba7"
    }

Block bao gồm 419 giao dịch và giao dịch thứ 64 (0627052b...) là giao dịch mua cà phê của Alice. Entry `height` cho chúng ta biết đây là block thứ 277316 trong blockchain.

### Dùng giao diện lập trình của Bitcoin Core

`bitcoin-cli helper` rất hữu ích trong việc tìm hiểu Bitcoin Core API và thử nghiệm các chức năng. Nhưng lý do chính của giao diện lập trình là để truy cập các chức năng qua lập trình. Trong phần này chúng ta sẽ demo truy cập Bitcoin Core từ một ngôn ngữ lập trình.

API của Bitcoin Core là một dạng giao diện JSON-RPC. JSON viết tắt cho *JavaScript Object Notation* và nó là một cách rất thuận tiện để biển diễn dữ liệu mà cả con người và chương trình lập trình đều có thể đọc một cách dễ dàng. Trong trường hợp này, network protocol là HTTP, hoặc HTTPS (cho kết nối bảo mật).

Khi sử dụng lệnh `bitcon-cli` để lấy *help* của một câu lệnh, nó sẽ chỉ cho chúng ta một ví dụ dùng `curl`, một command-line HTTP client linh hoạt để  tạo dựng những lệnh gọi JSON-RPC:

    $ curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/

Câu lệnh này diễn đạt `curl` submit một HTTP request tới local host (127.0.0.1), kết nối đến cổng bitcoin mặc định (8332), và submit jsonrpc request cho method `getinfo` dùng `text/plain` encoding.

Nếu bạn implement lệnh gọi JSON-RPC trong chương trình riêng, bạn có thể dùng một thư viện HTTP nào đó để xây dựng việc gọi này, giống như việc dùng `curl` trong ví dụ trên.

Tuy nhiên, có một số thư viện lập trình "wrap" Bitcoin Core API giúp cho mọi việc được dễ dàng. Chúng ta sẽ dùng thư viện `python-bitcoinlib` để đơn giản hóa việc truy cập API. Hãy nhớ rằng việc này đòi hỏi bạn phải chạy Bitcoin Core instance, thứ sẽ được dùng để tạo lệnh gọi JSON-RPC.

Script Python trong ví dụ **Chạy lệnh `getinfo` qua JSON-RPC API của Bitcoin Core** tạo một lệnh gọi `getinfo` đơn giản, in ra tham số của block từ dữ liệu trả về bởi Bitcoin Core.

Ví dụ 3. Chạy lệnh `getinfo` qua JSON-RPC API của Bitcoin Core

    link:code/rpc_example.py[]

Chạy lệnh này sẽ cho ra kết quả:

    $ python rpc_example.py
    394075

Nó nói cho chúng ta biết rằng bản local của Bitcoin Core node có 394075 block trong blockchain. Không phải một kết quả gì đặc sắc, nhưng nó giới thiệu cách dùng cơ bản của thư viện như một giao diện đơn giản hóa cho JSON-RPC API của Bitcoin Core.

Tiếp theo, hãy cùng dùng `getrawtransaction` và `decodetransaction` call để truy cập cụ thể thanh toán cốc cà phê của Alice. Trong ví dụ về **Truy cập một giao dịch và tạo output của nó**, chúng tra truy cập vào giao dịch của Alice và liệt kê tất cả output của giao dịch đó. Với mỗi output, chúng ta chỉ ra địa chỉ của người nhận và giá trị nhận. Hãy nhớ lại rằng giao dịch của Alice có một output trả cho Bob và một output tiền thừa trở lại Alice.

Ví dụ 4. Truy cập một giao dịch và tạo output của nó

    link:code/rpc_transaction.py[]

Chạy đoạn code này sẽ cho kết quả:

    $ python rpc_transaction.py
    ([u'1GdK9UzpHBzqzX2A9JFP3Di4weBwqgmoQA'], Decimal('0.01500000'))
    ([u'1Cdid9KFAaatwczBwBttQcwXYCpvK8h7FK'], Decimal('0.08450000'))

Cả hai ví dụ ở trên đều khá đơn giản. Bnaj không cần một chương trình lập trình để chạy chúng; bạn có thể đơn giản chỉ cần dùng `bitcoin-cli helper`. Tuy nhiên ví dụ tiếp theo sẽ cần vào trăm lệnh call RPC và demo rõ hơn việc dùng giao diện lập trình.

Trong ví dụ **Try cập một block và thêm tất cả output của giao dịch**, ban đầu chúng ta truy cập block 277316, sau đó truy cập từng giao dịch trong 419 giao dịch bên trong bằng cách tham chiếu tới mỗi ID của giao dịch. Sau đó, chúng ta khởi tạo output của mỗi giao dịch và cộng tổng giá trị lại.

Ví dụ 5. Try cập một block và thêm tất cả output của giao dịch

    link:code/rpc_block.py[]

Chạy đoạn code này sẽ cho kết quả:

    $ python rpc_block.py
    ('Total value in block: ', Decimal('10322.07722534'))

Đoạn code trong ví dụ tính toán tổng giá trị đã giao dịch trong block là 10,322.07722534 BTC (bao gồm 25 BTC reward và 0.0909 BTC fee). Hãy thử so sánh giá trị đó với một trang web block explorer nào đó bằng cách tìm theo block hash hoặc height. Một vài block explorer giá trị tổng đã loại bỏ reward và fee. Xem thử xem liệu bạn có thể tìm ra điểm khác biệt.

## Một số Client, Thư viện, và Toolkit thay thế

Trong hệ sinh thái bitcoin, có nhiều client, thư viện và toolkit thay thế, thậm chí có cả những implement cho full-node. Chúng được implemnt trong nhiều ngôn ngữ lập trình khác nhau, đóng góp vào giao diện lập trình native cho ngôn ngữ đó.

Sau đây là danh sách một số thư viện, client và toolkit tốt nhất hiện có, sắp xếp theo ngôn ngữ lập trình.

**C/C++**

[Bitcoin Core](https://github.com/bitcoin/bitcoin)

The reference implementation of bitcoin

[libbitcoin](https://github.com/libbitcoin/libbitcoin)

Cross-platform C++ development toolkit, node, and consensus library

[bitcoin explorer](https://github.com/libbitcoin/libbitcoin-explorer)

Libbitcoin's command-line tool

[picocoin](https://github.com/jgarzik/picocoin) 

A C language lightweight client library for bitcoin by Jeff Garzik

**JavaScript**

[bcoin](http://bcoin.io/)

A modular and scalable full-node implementation with API

[Bitcore](https://bitcore.io/)

Full node, API, and library by Bitpay

[BitcoinJS](https://github.com/bitcoinjs/bitcoinjs-lib)

A pure JavaScript Bitcoin library for node.js and browsers

**Java**

[bitcoinj](https://bitcoinj.github.io)

A Java full-node client library

[Bits of Proof (BOP)](https://bitsofproof.com)

A Java enterprise-class implementation of bitcoin

**Python**

[python-bitcoinlib](https://github.com/petertodd/python-bitcoinlib)

A Python bitcoin library, consensus library, and node by Peter Todd

[pycoin](https://github.com/richardkiss/pycoin)

A Python bitcoin library by Richard Kiss

[pybitcointools](https://github.com/vbuterin/pybitcointools)

A Python bitcoin library by Vitalik Buterin

**Ruby**

[bitcoin-client](https://github.com/sinisterchipmunk/bitcoin-client)

A Ruby library wrapper for the JSON-RPC API

**Go**

[btcd](https://github.com/btcsuite/btcd)

A Go language full-node bitcoin client

**Rust**

[rust-bitcoin](https://github.com/apoelstra/rust-bitcoin)

Rust bitcoin library for serialization, parsing, and API calls

**C#**

[NBitcoin](https://github.com/MetacoSA/NBitcoin)

Comprehensive bitcoin library for the .NET framework

**Objective-C**

[CoreBitcoin](https://github.com/oleganza/CoreBitcoin)

Bitcoin toolkit for ObjC and Swift

Nhiều thư viện khác tồn tại trong các ngôn ngữ khác và một số  thư viện mới luôn được tạo ra.

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