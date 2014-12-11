#实战出精华
用具体的C++网络编程例子来提升你的逼格

John Torjo

Boost.Asio C++ 网络编程

用具体的C++网络编程例子来提升你的逼格

Copyright © 2013 Packt Publishing

版权所有，在没有经过出版者事先的书面授权的情况下，除了在鉴定文章或评论中进行简单引用，该书的任何部分都不能被转载、存储在检索系统中、或者以任何形式和方式传阅。

虽然在本书准备发行之前，我们已经尽最大的努力去保证书中信息的准确性。但是，书中包含的明示或暗示的信息都不会提供保证。无论是本书作者、Packt Publishing以及其经销商和分销商都不承担由这本书造成的任何直接或间接的损失。

Packt Publishing将尽最大努力，用适当的大写来对书中提到的公司和产品进行商标标识。但是，Packt Publishing不能保证这些信息的准确性。

第一版发布：2013年1月

产品编号：1120213

由Packt Publishing Ltd.发布

工作人员

作者：John Torjo

协调人：Sherin Padayatty

评审：Béla Tibor Bartha、Nicolae Ghimbovschi

校对：Claire Cresswell-Lane

组稿编辑：Erol Staveley

索引编制：Monica Ajmera Mehta

责任编辑：Ameya Sawant

图像处理：Valentina D'silva、Aditi Gajjar

技术编辑：Kaustubh S. Mayekar

协调出版：Conidon Miranda

封面：Conidon Miranda

关于作者
做为一个权威的C++专家，在John Torjo超过15年的编程生涯中，他把大部分的时间都贡献给了C++。偶尔也会用C#和Java写程序。

他也很喜欢在C++ Users Journal和其他杂志上写一些关于编程的文章。

闲暇的时候，他喜欢玩扑克和开快车。他有很多自由职业，其中就有一个把他对扑克和编程的爱好结合起来。你可以通过john.code@torjo.com联系到他。

我要感谢我的朋友Alexandru Chis, Aurelian Hale, Bela Tibor Bartha, Cristian Fatu, Horia Uifaleanu, Nicolae Ghimbovschi以及Ovidiu Deac对本书提出的反馈和意见。同时我也要感谢Packt各位的对我时不时错过截稿日期行为的理解。然后最需要感谢的是Chris Kohlhoff，Boost.Asio的作者，是他写出了一个如此伟大的库。

把这本书献给我最好的朋友Darius。

关于评审员
Béla Tibor Bartha

一个用各种技术和语言进行工作的专业软件工程师。尽管在过去的4年里，他做的是iOS和OSX应用开发，但是C++陪伴他度过了他早期个人游戏项目开发的激情岁月。

我要感谢John，因为他我才能做这本书的评审

Nicolae Ghimbovschi

一个参加各种各样的C++项目超过5年的天才个人开发者。他主要参与一些企业通信工程的项目。他是一个狂热的Linux爱好者，他喜欢利用不同的操作系统、脚本工具、编程语言进行测试和实验。除了编程，他还喜欢骑自行车、瑜伽和冥想。

我要感谢John让我来评审这本书

目录
前言

第一章：Boost.Asio入门

什么是Boost.Asio？
    历史
    依赖
    编译 Boost.Asio
    重要的宏
同步VS异步
异常VS错误代码
Boost.Asio中的多线程
不仅仅是网络
计时器
io_service类
第二章：Boost.Asio基本原理

网络API
Boost.Asio命名空间
IP地址
端点
Sockets
    同步错误代码
    Socket成员函数
    其他注意事项
read/write/connect自由函数
    connect函数
    read/write函数
异步编程
    为什么要异步？
    异步run(),run_one(),poll(),poll_one()
        持续运行
        run_one(),poll(),poll_one()函数
    异步工作
    异步post() VS dispatch() VS wrap()
保持运行
总结
第三章：回显服务端/客户端

TCP回显服务端/客户端
    TCP同步客户端
    TCP同步服务端
    TCP异步客户端
    TCP同步服务端
    代码
UDP回显服务端/客户端
    UDP同步回显客户端
    UDP同步回显服务端
总结
第四章：客户端和服务端

同步客户端/服务端
    同步客户端
    同步服务端
异步客户端/服务端
    异步客户端
    异步服务端
总结
第五章：同步VS异步

同步异步混合编程
客户端和服务端之间消息的互相传递
客户端软件中的同步I/O
服务端软件中的同步I/O
    同步服务端中的线程
客户端软件中的异步I/O
服务端软件中的异步I/O
    异步服务端中的线程
异步操作
代理实现
总结
第六章：Boost.Asio-其他特性

std streams和std buffer I/O
Boost.Asio和STL流
streambuf类
处理streambuf对象的自由函数
协程
总结
第七章：Boost.Asio-进阶

Asio VS Boost.Asio
调试
    处理程序跟踪信息
    例子
    处理程序跟踪文件
SSL
Boost.Asio的Windows特性
    流处理
    随机存储处理
    对象处理
Boost.Asio的POSIX特性
    本地sockects
    连接本地sockets
    POSIX文件描述符
    Fork
    总结
索引

前言
网络编程由来已久，并且是一个极富挑战性的任务。Boost.Asio对网络编程做了一个极好的抽象，从而保证你用少量的编程就可以创造出一个优雅的客户端-服务端软件。并在创造的过程中，它能让你体会到极大的乐趣。而更为有益的是：Boost.Asio包含了一些非网络的特性，用Boost.Asio写出来的代码紧凑、易读，而且如果你按照我在书中所讲的来做，你的代码会无懈可击。

这本书涵盖了什么？

第一章：Boost.Asio入门将告诉你Boost.Asio是什么？怎么编译它？顺带着会有一些例子。你会发现Boost.Asio不仅仅是一个网络库。同时你也会接触到Boost.Asio中最核心的类io_service。

第二章：Boost.Asio基本原理包含了你必须了解的内容：什么时候用Boost.Asio？我们将深入了解异步编程——一种比同步更需要技巧，且更有乐趣的编程方式。这一章也是在开发你自己的网络应用时需要回过头，把里面的内容作为参考的一章。

第三章：回显服务端/客户端将会告诉你如何实现一个小的客户端-服务端应用；也许，这会是你写过的最简单的客户端-服务端应用。回显应用就是一个把客户端发过来的任何消息发送回去然后关闭客户端连接的服务。我们会先实现一个同步的应用，然后再实现一个异步的应用，这样你就可以非常容易地看到它们之间的不同。

第四章：客户端和服务端会深入讨论如何用Boost.Asio创建一个简单的客户端－服务端应用。我们将讨论如何避免诸如内存泄漏和死锁的缺陷。所有的程序都是简单的框架，从而使你更方便的对他们进行扩展并满足你的需求。

第五章：同步VS异步会带你了解那些当你选择同步还是异步方式时需要考虑的事情。首先就是避免混淆它们。在这一章，我们会发现每个类型应用的实现、测试和调试是多么的容易。

第六章：Boost.Asio的其他特性将带你了解Boost.Asio一些不为人知的特性。你会发现，虽然std streams和streambufs有一点点难用，但是却表现出了它们得天独厚的优势。最后，你会看到姗姗来迟的Boost.Asio协程的入口，它可以让你用一种更易读的方式来写异步代码。（就好像它是同步的一样）

第七章：Boost.Asio进阶会处理一些Boost.Asio的进阶问题。虽然在日常编程中你不需要深入研究它们，但是了解它们对你有益无害（Boost.Asio高级调试，SSL，Windows特性，POSIX特性等）。

读这本书你需要准备什么？

为了编译Boost.Asio以及运行本书中的例子，你需要一个现代编译器。例如，Visual Studio 2008及其以上版本或者g++ 4.4及其以上版本

这本书是为谁准备的？

这本书对于那些需要进行网络编程却不想深入研究复杂的原始网络API的开发者来说是一个福音。所有你需要的只是Boost.Asio提供的一个简单抽象。作为著名的Boost C++库的一部分，你只需要额外添加几个#include文件即可转换到Boost.Asio。

在读这本书之前，你需要熟悉Boost核心库的一些知识，例如Boost智能指针、boost::noncopyable、Boost Functors、Boost Bind、shared_ from_this/enabled_shared_from_this和Boost线程（线程和互斥量）。同时还需要了解Boost的Date/Time。读者还需要知道阻塞的概念以及“非阻塞”操作。

约定

你会发现本书中用不同样式的文字来区分不同种类的信息。这里给出这些样式的例子以及它们的解释。

文本中的代码会这样显示：“通常一个io_service的例子就足够了”。

一段代码是下面这个样子的：

read(stream, buffer [, extra options])

async_read(stream, buffer [, extra options], handler)

write(stream, buffer [, extra options])

async_write(stream, buffer [, extra options], handler)
专业词汇和重要的单词用黑体显示

[！警告或者重要的注释在这样的一个框里面]

[？技巧在这样的一个框里面]

读者反馈

我们欢迎来自读者的反馈。告诉我们你对这本书的看法——你喜欢哪部分，不喜欢哪部分。读者的反馈对我们非常重要，它能让我们写出对读者帮助最大的书籍。

你只需要发送一封邮件到feedback@packtpub.com即可进行一般的反馈，注意在邮件的主题中注明书名。

如果你有一个擅长的专题，想撰写一本书或者为某本书做贡献。请阅读我们在www.packtpub.com/authors上的作者指引。

用户支持

现在你已经是Packt书籍的拥有者，我们将告诉你一些事项，让你购买本书得到的收益最大化。

下载示例代码

你可以在http://www.packtpub.com登录你的帐号，然后下载你所购买的书籍的全部示例代码。同时，你也可以通过访问http://www.packtpub.com/support进行注册，然后这些示例代码文件将直接发送到你的邮箱。

纠错

尽管我们已经尽最大的努力去保证书中内容的准确性，但是错误始终是存在的。如果你在我们的书籍中发现了错误——也许是文字，也许是代码——如果你能将它们报告给我们，我们将不胜感激。这样的话，你不仅能让帮助其他读者避免一些疑惑，同时也能帮助我们改进这本书的下一个版本。如果你发现任何需要纠正的地方，访问http://www.packtpub.com/submit-errata，选择你的书籍，点击errata submission form链接，然后输入详细的纠错信息来将错误报告给我们。一经确定，你的提交就会通过并且纠错会上传到我们的网站，或者添加到那本书的纠错信息区域的纠错列表中。所有存在的纠错都可以访问http://www.packtpub.com/support，然后通过选择书名的方式来查看。

盗版

在互联网上通过各种媒体盗版版权材料是个一直存在的问题。在Packt，版权和许可的保护非常严格。如果你在互联网上发现任何形式的关于我们作品的非法备份。请及时把链接或者网址反馈给我们以便我们采取补救措施。

请将可疑盗版材料的链接通过copyright@packtpub.com发送给我们。 对于你帮助我们保护我们的作者以及我们提供有价值内容能力的行为我们将不胜感激。

答疑

如果你有关于本书任何方面的问题，你可以通过questions@packtpub.com联系我们。我们将尽我们最大的努力进行解答

Boost.Asio入门
首先，让我们先了解Boost.Asio是什么？怎么编译它？顺带着会有一些例子。你会发现Boost.Asio不仅仅是一个网络库。同时你也会接触到Boost.Asio中最核心的类io_service。

什么是Boost.Asio

简单来说，Boost.Asio是一个跨平台的、主要用于网络和其他一些底层输入/输出编程的C++库。

计算机网络的设计方式有很多种，但是Boost.Asio的的方式远远优于它们。它在2005年就被包含进Boost，然后被大量Boost的用户测试并在很多项目中使用，比如Remobo(http://www.remobo.com)，可以让你创建你自己的即时私有网络(IPN)，libtorrent(http://www.rasterbar.com/products/libtorrent)一个实现了比特流客户端的库，PokerTH (http://www.pokerth.net)一个支持LAN和互联网对战的纸牌游戏。

Boost.Asio在网络通信、COM串行端口和文件上成功地抽象了输入输出的概念。你可以基于这些进行同步或者异步的输入输出编程。

read(stream, buffer [, extra options])
async_read(stream, buffer [, extra options], handler)
write(stream, buffer [, extra options])
async_write(stream, buffer [, extra options], handler)
从前面的代码片段可以看出，这些函数支持传入包含任意内容（不仅仅是一个socket，我们可以对它进行读写）的流实例。

作为一个跨平台的库，Boost.Asio可以在大多数操作系统上使用。能同时支持数千个并发的连接。其网络部分的灵感来源于伯克利软件分发(BSD)socket，它提供了一套可以支持传输控制协议(TCP)socket、用户数据报协议(UDP)socket和Internet控制消息协议(IMCP)socket的API，而且如果有需要，你可以对其进行扩展以支持你自己的协议。

历史

Boost.Asio在2003被开发出来，然后在2005年的12月的Boost 1.35版本中引入。原作者是Christopher M. Kohlhoff，你可以通过chris@kohlhoff.com联系他。

这个库在如下的平台和编译器上测试通过：

32-bit和64-bit Windows，使用Visual C++ 7.1及以上

Windows下使用MinGW

Windows下使用Cygwin(确保已经定义 __USE_232_SOCKETS)

基于2.4和2.6内核的Linux，使用g++ 3.3及以上

Solaris下使用g++ 3.3及以上

MAC OS X 10.4以上下使用g++ 3.3及以上

它或许能在诸如AIX 5.3，HP-UX 11i v3，QNX Neutrino 6.3，Solaris下使用Sun Studio 11以上，True64 v5.1，Windows下使用Borland C++ 5.9.2以上等平台上使用。（更多细节请咨询www.boost.org）

依赖

Boost.Asio依赖于如下的库：

Boost.System：这个库为Boost库提供操作系统支持(http://www.boost.org/doc/libs/1_51_0/doc/html/boost_system/index.html)
Boost.Regex：使用这个库（可选的）以便你重载read_until()或者async_read_until()时使用boost::regex参数。

Boost.DateTime：使用这个库（可选的）以便你使用Boost.Asio中的计时器。

OpenSSL：使用这个库（可选的）以便你使用Boost.Asio提供的SSL支持。

编译Boost.Asio

Boost.Asio是一个仅有头文件的库。然而，根据你的编译器和你程序的大小，你可以选择用源文件的方式来编译Boost.Asio。如果你想要这么做以减少编译时间，有如下几种方式：

在你的一个源文件中，添加#include "boost/asio/impl/src.hpp"（如果你在使用SSL，添加#include "boost/asio/ssl/impl/src.hpp"）
在你所有的源文件中，添加#define BOOST_ASIO_SEPARATE_COMPILATION

注意Boost.Asio依赖于Boost.System，必要的时候还依赖于Boost.Regex，所以你需要用如下的指令先编译Boost：

bjam –with-system –with-regex stage

如果你还想同时编译tests，你需要使用如下的指令：

bjam –with-system –with-thread –with-date_time –with-regex –with-serialization stage

这个库有大量的例子，你可以连同这本书中的例子一块看看。

重要的宏

如果设置了BOOST_ASIO_DISABLE_THREADS；Boost.Asio中的线程支持都会失效，不管在编译Boost的过程中是否使用了线程支持。

同步VS异步

首先，异步编程和同步编程是有极大的不同的。在同步编程中，你所有的操作都是顺序执行的，比如从一个socket中读取（请求），然后写入（回应）到socket中。每一个操作操作都是阻塞的。因为操作是阻塞的，所以为了不影响主程序，当读写一个socket时，通常创建一个或多个线程来处理socket的输入/输出。因此，同步的服务端/客户端通常是多线程的。

相反的，异步编程是事件驱动的。虽然你启动了一个操作，但是你不知道它何时会结束；你只是提供一个回调，当操作结束时，它会调用这个API，并返回操作结果。对于有着丰富经验的QT（诺基亚用来创建跨平台图形用户界面应用程序的库）程序员来说，这就是他们第二天性。因此，在异步编程中，你只需要一个线程。

因为中途做改变会非常困难而且容易出错，所以你在项目初期（最好是一开始）就得决定用同步还是异步的方式实现网络通信。不仅API有极大的不同，你程序的语意也会完全改变（异步网络通信通常比同步网络通信更加难以测试和调试）。你需要考虑是采用阻塞调用和多线程的方式（同步，通常比较简单），或者是更少的线程和事件驱动（异步，通常更复杂）。

下面是一个基础的同步客户端例子：

using boost::asio;
io_service service;
ip::tcp::endpoint ep( ip::address::from_string("127.0.0.1"), 2001);
ip::tcp::socket sock(service);
sock.connect(ep);
首先，你的程序至少需要一个io_service实例。Boost.Asio使用io_service同操作系统的输入/输出服务进行交互。通常一个io_service的实例就足够了。然后，创建你想要连接的地址和端口，再建立socket。把socket连接到你创建的地址和端口。

下面是一个简单的使用Boost.Asio的服务端：

typedef boost::shared_ptr<ip::tcp::socket> socket_ptr;
io_service service;
ip::tcp::endpoint ep( ip::tcp::v4(), 2001)); // listen on 2001
ip::tcp::acceptor acc(service, ep);
while ( true) {
    socket_ptr sock(new ip::tcp::socket(service));
    acc.accept(*sock);
    boost::thread( boost::bind(client_session, sock));
}
void client_session(socket_ptr sock) {
    while ( true) {
        char data[512];
        size_t len = sock->read_some(buffer(data));
        if ( len > 0)
            write(*sock, buffer("ok", 2));
    }
}
首先，同样是至少需要一个io_service实例。然后你指定你想要监听的端口，再创建一个接收器——一个用来接收客户端连接的对象。 在接下来的循环中，你创建一个虚拟的socket来等待客户端的连接。然后当一个连接被建立时，你创建一个线程来处理这个连接。

在client_session线程中来读取一个客户端的请求，进行解析，然后返回结果。

而创建一个异步的客户端，你需要做如下的事情：

using boost::asio;
io_service service;
ip::tcp::endpoint ep( ip::address::from_string("127.0.0.1"), 2001);
ip::tcp::socket sock(service);
sock.async_connect(ep, connect_handler);
service.run();
void connect_handler(const boost::system::error_code & ec) {
    // 如果ec返回成功我们就可以知道连接成功了
}
在程序中你需要至少创建一个io_service实例。你需要指定连接的地址以及创建socket。

当连接完成时（其完成处理程序）你就异步地连接到了指定的地址和端口，也就是说，connect_handler被调用了。

当connect_handler被调用时，检查错误代码（ec），如果成功，你就可以向服务端进行异步的写入。

注意：只要还有待处理的异步操作，servece.run()循环就会一直运行。在上述例子中，只执行了一个这样的操作，就是socket的async_connect。在这之后，service.run()就退出了。

每一个异步操作都有一个完成处理程序——一个操作完成之后被调用的函数。 下面的代码是一个基本的异步服务端

using boost::asio;
typedef boost::shared_ptr<ip::tcp::socket> socket_ptr;
io_service service;
ip::tcp::endpoint ep( ip::tcp::v4(), 2001)); // 监听端口2001
ip::tcp::acceptor acc(service, ep);
socket_ptr sock(new ip::tcp::socket(service));
start_accept(sock);
service.run();
void start_accept(socket_ptr sock) {
    acc.async_accept(*sock, boost::bind( handle_accept, sock, _1) );
}
void handle_accept(socket_ptr sock, const boost::system::error_code &
err) {
    if ( err) return;
    // 从这里开始, 你可以从socket读取或者写入
    socket_ptr sock(new ip::tcp::socket(service));
    start_accept(sock);
}
在上述代码片段中，首先，你创建一个io_service实例，指定监听的端口。然后，你创建接收器acc——一个接受客户端连接，创建虚拟的socket，异步等待客户端连接的对象。

最后，运行异步service.run()循环。当接收到客户端连接时，handle_accept被调用（调用async_accept的完成处理程序）。如果没有错误，这个socket就可以用来做读写操作。

在使用这个socket之后，你创建了一个新的socket，然后再次调用start_accept()，用来创建另外一个“等待客户端连接”的异步操作，从而使service.run()循环一直保持忙碌状态。

异常处理VS错误代码

Boost.Asio允许同时使用异常处理或者错误代码，所有的异步函数都有抛出错误和返回错误码两种方式的重载。当函数抛出错误时，它通常抛出boost::system::system_error的错误。

using boost::asio;
ip::tcp::endpoint ep;
ip::tcp::socket sock(service);
sock.connect(ep); // 第一行
boost::system::error_code err;
sock.connect(ep, err); // 第二行
在前面的代码中，sock.connect(ep)会抛出错误，sock.connect(ep, err)则会返回一个错误码。

看一下下面的代码片段：

try {
    sock.connect(ep);
} catch(boost::system::system_error e) {
    std::cout << e.code() << std::endl;
}
下面的代码片段和前面的是一样的：

boost::system::error_code err;
sock.connect(ep, err);
if ( err)
    std::cout << err << std::endl;
当使用异步函数时，你可以在你的回调函数里面检查其返回的错误码。异步函数从来不抛出异常，因为这样做毫无意义。那谁会捕获到它呢？

在你的异步函数中，你可以使用异常处理或者错误码（随心所欲），但要保持一致性。同时使用这两种方式会导致问题，大部分时候是崩溃（当你不小心出错，忘记去处理一个抛出来的异常时）。如果你的代码很复杂（调用很多socket读写函数），你最好选择异常处理的方式，把你的读写包含在一个函数try {} catch块里面。

void client_session(socket_ptr sock) {
    try {
        ...
    } catch ( boost::system::system_error e) {
        // 处理错误
    }
}
如果使用错误码，你可以使用下面的代码片段很好地检测连接是何时关闭的：

char data[512];
boost::system::error_code error;
size_t length = sock.read_some(buffer(data), error);
if (error == error::eof)
    return; // 连接关闭
Boost.Asio的所有错误码都包含在boost::asio::error的命名空间中（以便你创造一个大型的switch来检查错误的原因）。如果想要了解更多的细节，请参照boost/asio/error.hpp头文件。

Boost.Asio中的线程

当说到Boost.Asio的线程时，我们经常在讨论：

io_service:io_service是线程安全的。几个线程可以同时调用io_service::run()。大多数情况下你可能在一个单线程函数中调用io_service::run()，这个函数必须等待所有异步操作完成之后才能继续执行。然而，事实上你可以在多个线程中调用io_service::run()。这会阻塞所有调用io_service::run()的线程。只要当中任何一个线程调用了io_service::run()，所有的回调都会同时被调用；这也就意味着，当你在一个线程中调用io_service::run()时，所有的回调都被调用了。
socket:socket类不是线程安全的。所以，你要避免在某个线程里读一个socket时，同时在另外一个线程里面对其进行写入操作。（通常来说这种操作都是不推荐的，更别说Boost.Asio）。
utility:就utility来说，因为它不是线程安全的，所以通常也不提倡在多个线程里面同时使用。里面的方法经常只是在很短的时间里面使用一下，然后就释放了。
除了你自己创建的线程，Boost.Asio本身也包含几个线程。但是可以保证的是那些线程不会调用你的代码。这也意味着，只有调用了io_service::run()方法的线程才会调用回调函数。

不仅仅是网络通信

除了网络通信，Boost.Asio还包含了其他的I/O功能。

Boost.Asio支持信号量，比如SIGTERM（软件终止）、SIGINT（中断信号）、SIGSEGV（段错误）等等。 你可以创建一个signal_set实例，指定异步等待的信号量，然后当这些信号量产生时，就会调用你的异步处理程序：

void signal_handler(const boost::system::error_code & err, int signal)
{
    // 纪录日志，然后退出应用
}
boost::asio::signal_set sig(service, SIGINT, SIGTERM);
sig.async_wait(signal_handler);
如果SIGINT产生，你就能在你的signal_handler回调中捕获到它。

你可以使用Boost.Asio轻松地连接到一个串行端口。在Windows上端口名称是COM7，在POSIX平台上是/dev/ttyS0。

io_service service;
serial_port sp(service, "COM7");
打开端口后，你就可以使用下面的代码设置一些端口选项，比如端口的波特率、奇偶校验和停止位。

serial_port::baud_rate rate(9600);
sp.set_option(rate);
打开端口后，你可以把这个串行端口看做一个流，然后基于它使用自由函数对串行端口进行读/写操作。比如async_read(), write, async_write(), 就像下面的代码片段：

char data[512];
read(sp, buffer(data, 512));
Boost.Asio也可以连接到Windows的文件，然后同样使用自由函数，比如read(), asyn_read()等等，就像下面的代码片段：

HANDLE h = ::OpenFile(...);
windows::stream_handle sh(service, h);
char data[512];
read(h, buffer(data, 512));
对于POXIS文件描述符，比如管道，标准I/O和各种设备（但不包括普通文件）你也可以这样做，就像下面的代码所做的一样：

posix::stream_descriptor sd_in(service, ::dup(STDIN_FILENO));
char data[512];
read(sd_in, buffer(data, 512));
计时器

一些I/O操作需要一个超时时间。这只能应用在异步操作上（同步意味着阻塞，因此没有超时时间）。例如，你的下一条信息必须在100毫秒内从你的同伴那传递给你。

bool read = false;
void deadline_handler(const boost::system::error_code &) {
    std::cout << (read ? "read successfully" : "read failed") << std::endl;
}
void read_handler(const boost::system::error_code &) {
    read = true;
}
ip::tcp::socket sock(service);
…
read = false;
char data[512];
sock.async_read_some(buffer(data, 512));
deadline_timer t(service, boost::posix_time::milliseconds(100));
t.async_wait(&deadline_handler);
service.run();
在上述代码片段中，如果你在超时之前读完了数据，read则被设置成true，这样我们的伙伴就及时地通知了我们。否则，当deadline_handler被调用时，read还是false，也就意味着我们的操作超时了。

Boost.Asio也支持同步计时器，但是它们通常和一个简单的sleep操作是一样的。boost::this_thread::sleep(500);这段代码和下面的代码片段完成了同一件事情：

deadline_timer t(service, boost::posix_time::milliseconds(500));
t.wait();
io_service类

你应该已经发现大部分使用Boost.Asio编写的代码都会使用几个iosservice的实例。ios_service是这个库里面最重要的类；它负责和操作系统打交道，等待所有异步操作的结束，然后为每一个异步操作调用完成处理程序。 如果你选择用同步的方式来创建你的应用，你不需要考虑我将在这一节向你展示的东西。 你可以用几种不同的方式来使用io_service。在下面的例子中，我们有3个异步操作，2个socket连接和一个计时器等待： 有一个io_service和一个处理线程的单线程例子： io_service service; // all the socket operations are handled by service ip::tcp::socket sock1(service); // all the socket operations are handled by service ip::tcp::socket sock2(service); sock1.asyncconnect( ep, connect_handler); sock2.async_connect( ep, connect_handler); deadline_timer t(service, boost::posixtime::seconds(5)); t.async_wait(timeout_handler); service.run(); 有单个ioservice实例和多个处理线程的多线程例子： io_service service; ip::tcp::socket sock1(service); ip::tcp::socket sock2(service); sock1.asyncconnect( ep, connect_handler); sock2.async_connect( ep, connect_handler); deadline_timer t(service, boost::posixtime::seconds(5)); t.async_wait(timeout_handler); for ( int i = 0; i < 5; ++i) boost::thread( run_service); void run_service() { service.run(); } 有多个ioservice实例和多个处理线程的多线程例子： io_service service[2]; ip::tcp::socket sock1(service[0]); ip::tcp::socket sock2(service[1]); sock1.asyncconnect( ep, connect_handler); sock2.async_connect( ep, connect_handler); deadline_timer t(service[0], boost::posixtime::seconds(5)); t.async_wait(timeout_handler); for ( int i = 0; i < 2; ++i) boost::thread( boost::bind(run_service, i)); void run_service(int idx) { service[idx].run(); } 首先，要注意你不能拥有多个ioservice却只有一个线程。下面的代码片段没有任何意义： for ( int i = 0; i < 2; ++i) service[i].run(); 上面的代码片段没有意义是因为service[1].run()需要service[0].run()先结束。因此，所有由service[1]处理的异步操作都需要等待，这显然不是一个好主意。 在前面的3个方案中，我们在等待3个异步操作结束。为了解释之间的不同点，我们假设：过一会操作1完成，然后接着操作2完成。同时我们假设每一个完成处理程序需要1秒钟来完成执行。 在第一个例子中，我们在一个线程中等待三个操作全部完成，只要第1个操作完成，我们调用它的完成处理程序。尽管操作2紧接着完成了，操作2的完成处理程序需要在1秒钟后操作1的完成处理程序完成才被调用。 第二个例子，我们在两个线程中等待3个异步操作结束。当操作1完成时，我们在第一个线程中调用它的完成处理程序。当操作2完成时，紧接着，我们就在第二个线程中调用它的完成处理函数（当线程1在忙着响应操作1的处理程序时，线程2空闲着并且可以回应任何新进来的操作）。 在第三个例子中，因为操作1是sock1的connect，操作2是sock2的connect，所以应用程序会表现得像第二个例子一样。线程1会处理sock1 connect操作的完成处理程序，线程2会处理sock2的connect操作的完成处理程序。然而，如果sock1的connect操作是操作1，deadline_timer t的超时操作是操作2，线程1会结束正在处理的sock1 connect操作的完成处理程序。因而，deadline_timer t的超时操作必须等sock1 connect操作的完成处理程序结束（等待1秒钟），因为线程1要处理sock1的连接处理程序和t的超时处理程序。 下面是你需要从前面的例子中学到的： 第一种情况是非常基础的应用程序。因为是串行的方式，所以当几个处理程序要被同时调用时，你会经常遇到瓶颈。如果一个处理程序需要花费很长的时间来执行，所有随后的处理程序都不得不等待。 第二种情况是比较适用的应用程序。他是非常强壮的——如果几个处理程序被同时调用了（这是有可能的），它们会在各自的线程里面被调用。唯一的瓶颈就是所有的处理线程都很忙的同时又有新的处理程序被调用。然而，这有快速的解决方式，增加处理线程的数目即可。 第三种情况最复杂和最难理解的。你只有在第二种情况不能满足需求时才使用它。这种情况一般就是当你有成千上万实时（socket）连接时。你可以认为每一个处理线程（运行io_service::run()的线程）有它自己的select/epoll循环；它等待任何一个socket，然后监控一个读写操作，当它发现这种操作时，就执行。大部分情况下，你不需要担心什么，唯一你需要担心的就是当你监控的socket数目以指数级的方式增长时（超过1000个的socket）。在那种情况下，有几个select/epoll循环会增加响应时间。 如果你觉得你成应用程序可能需要转换到第三种模式，请确保监听操作的这段代码（调用io_service::run()的代码）和应用程序其他部分是隔离的，这样你就可以很轻松的对其进行更改。 最后，要一直记住如果没有其他需要监控的操作，.run()就会结束，就像下面给的代码片段： io_service service; tcp::socket sock(service); sock.async_connect( ep, connect_handler); service.run(); 在上面的例子，只要sock建立了一个连接，connecthandler就会被调用，然后接着service.run()就会完成执行。 如果你想要service.run()接着执行，你需要分配更多的工作给它。这里有两个方式来完成这个目标。一种方式是在connect_handler中启动另外一个异步操作来分配更多的工作。 另一种方式模拟一些工作给它，用下面的代码片段： typedef boost::shared_ptr work_ptr; work_ptr dummy_work(new io_service::work(service)); 上面的代码可以保证service.run()一直运行直到你调用useservice.stop()或者 dummy_work.reset(0);// 销毁 dummy_work.

总结 Boost.Asio是一个复杂的库，但是却让网络编程变得异常简单。编译它很简单。它避免使用宏，这一点做得很好；他虽然定义了少部分的宏来做选项开关，但是你需要担心的很少。 Bosot.Asio支持同步和异步编程。他们有很大不同；你需要早早地选择其中的一种，因为它们之间的转换是非常复杂而且易错的。 如果你选择同步，你可以选择异常处理或者错误码，从异常处理转到错误码；只需要在call函数中增加一个参数即可（错误码）。 Boost.Asio不仅仅可以用来做网络编程。它还有其他更多的特性，这让它显得更有价值，比如信号量，计时器等等。 下一章我们将深入研究大多数Boost.Asio中用来做网络编程的函数和类。同时我们也会学一些异步编程的诀窍。