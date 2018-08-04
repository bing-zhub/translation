# Node-RED:讲座4 – 浏览核心节点

本讲座将介绍Node-RED默认安装的核心节点，然后向您展示基于云的Node RED服务（FRED）支持的扩展节点。

对于每个节点，您将看到其功能的简要概述，并指出本讲座系列中的哪个示例使用该节点，以便您可以更详细地查看如何使用该节点。 本讲座主要是参考部分。 但是，您可以快速浏览节点，以便在开始制作自己的流程时，了解您可以使用的基本功能。

## Node-RED的默认节点集

当您在Raspberry Pi或Beagleboard等设备上安装Node-RED时，会启动一组默认的节点。 默认安装中有8个主要类别的节点：输入，输出，功能，社交，存储，分析，高级和Raspberry Pi（见图4.1和4.2）让我们再来看看每个类别。

![http://noderedguide.com/wp-content/uploads/2015/10/Node-RED-Lecture-4-A-tour-of-the-core-nodes-41.jpg](file:////Users/bing/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image001.png)

图4.1默认输入，输出，功能和社交媒体节点。

## 输入节点

默认情况下安装了7个基本输入节点。 它们涵盖了物联网应用程序可能使用的基本通信机制。 从较低级别的互联网协议（如UDP和TCP）到高级HTTP以及发布/订阅MQTT。

| 节点名称 | 简述 | 样例 |
| ----- | ------------ | ----------- |
| inject | 将时间戳或用户配置的文本注入到消息中。  可以配置为手动注入，以设置的间隔或特定时间（使用Cron）进行注入。 | Examples 2.1, 3.6, 3.7, 3.8, 5.1-5.4, 6.1-6.8 |
| catch | 捕获相同选项卡上的节点抛出的错误。  如果节点在处理消息时引发错误，则流程通常会停止。  该节点可用于捕获返回消息的错误，并显示错误属性，详细说明错误以及源节点和类型。| Examples |
| mqtt | 订阅MQTT代理并监听主题，将主题上发布的任何数据作为新消息返回。  支持服务质量水平设置和最后的数据保留. | Examples 3.1-3.5 |
| http | 接收HTTP请求，允许Node-RED充当基本的Web服务器。 HTTP身份作为输出消息以及任何响应传递。  消息可以包含标准的URL编码数据或JSON。| Example 1.3, 5.7|
| websocket| 为浏览器提供一个端点，以建立与Node-RED的Websocket连接。  提供浏览器/服务器组合的双工连接。| Example 3.7 |
| tcp | 用于接受指定端口上的传入TCP请求或连接到远程TCP端口。  将包含TCP数据的消息生成为缓冲区，字符串或base64编码的单个或多个流。| Examples lecture 7|
| udp | 用于接收指定端口上的传入UDP数据包（或组播数据包）。  生成包含UDP数据的消息作为缓冲，字符串或base64编码的字符串。| Examples lecture 7 |
| serial in | 从本地设备上的串行端口读取。  可以配置为读取缓冲区，在特定的时间段或等待换行。| Examples lecture 7 |

## 输出节点

输出节点基本上是输入节点的基本集合的镜像，并提供了一种在同一组协议（即mqtt，http，udp等）上发送数据的方法。

| 节点名称 | 简述 | 样例 |
| --- | --- | --- |
| debug | 提供一种查看调试窗格中显示的消息的简单方法。  可以配置为仅显示msg.payload或整个msg对象。 | Various, examples 2.1, 2.2, 3.1-3.6, 5.1-5.4, 6.1-6.5 |
| mqtt | 订阅一个MQTT代理，并将其在传入消息中接收的任何数据（msg.payload）发布到主题。  支持服务质量水平和最后的数据保留。| Example 3.6 | 
| http | 将响应发送回HTTP输入节点收到的HTTP请求。  响应主体由msg.payload确定，并且可以定义标题和状态代码。 | Examples |
| websocket | 在配置的websocket上发送msg.payload。  如果定义了msg. session，则发送给始发客户端，否则广播到所有连接的客户端 | Example 3.7 |
| tcp | 回复配置的TCP端口。  也可以用来发送到特定端口。| Example 3.8|
| udp | 向配置的主机（IP地址）和端口发送UDP消息。  支持广播  像大多数节点一样，通过UI或消息属性进行配置。| Examples |
| serial out | 发送到定义的串行端口。  可以配置为在任何消息有效载荷之后发送可选的换行符。| Examples lecture 7 |

## 功能节点

 功能类别包含执行特定处理功能的各种节点。 这些范围从简单的延迟和切换节点到可编程功能节点，可以适应几乎任何编程需要。

| 节点名称 | 简述 | 样例 |
| --- | --- | --- |
| function| 通用可编程功能节点。  使用标准JavaScript语法，节点可以被定制以对其生成一个或多个输出消息的输入消息进行复杂处理。| Examples 2.1, 2.2, 3.8, 5.1-5.4, 5.7, 6.1-6.8|
| template | 配置了一个任意复杂的模板（使用胡塞尔格式），该节点接收一个包含名称：值对的输入消息并将其插入到模板中。  用于构建邮件，HTML，配置文件等 | Example 1.3|
| delay | 一种通过特定方法或随机时间延迟消息的通用节点。  也可以配置为限制消息流（例如每秒10 msg）。| Examples 5.6, 6.8 |
| trigger | 每当接收到输入消息时，创建两个输出消息，间隔可配置的时间间隔。  也可以用作监控定时器。| Example 1.1 |
| comment | 一个简单的视觉评论配置了标题和主体。 | Example 2.1 |
| http request | 允许您构建并发送HTTP请求到特定的URL。  方法（PUT，GET等），标题和有效载荷都可以通过UI或以编程方式进行配置. | Examples 1.3, 6.1, 6.6 |
| tcp request | 一个简单的TCP请求节点。  它将msg.payload发送到服务器tcp端口，并期望响应。  可以配置等待数据，等待特定字符，或立即返回。 | Example 3.8 |
| switch | 该节点根据其属性路由消息。  属性使用UI进行配置，并且可以是应用于消息属性的各种逻辑（>，<，\> =等）。| Examples 3.2-3.5, 5.5 |
| change | 更改节点可用于设置，更改或删除传入邮件的属性。  各种可配置规则允许复杂的更改，包括msg.payload中的搜索和替换 | Examples  3.3-3.5|
| range| 一个简单的缩放节点，将数字输入映射到新的输出。  适用于输入值的转换或界限范围，例如  温度。  未定义的非数字数据。| Example 3.5|
| csv| 该节点解析msg.payload并尝试转换为/从CSV转换。  如果它接收到一个字符串，它会输出一个JavaScript对象，如果它接收到一个JavaScript对象，它将输出一个CSV字符串。 | Examples |
| html| 使用可配置的选择器（CSS选择器语法）从msg.payload中的html文档中提取元素。  本质上允许您解析HTML并返回匹配的元素的数组。 | Example 6.1 |
| json | 此节点转换为/从JSON对象。  如果它收到一个JavaScript对象，它会输出JSON，如果它接收到JSON，它将输出一个JavaScript对象。 | Examples 3.1-3.5, 5.7, 6.6 |
| xml | 此节点转换为/从XML格式转换。  如果它接收到一个JavaScript对象，它会输出一个XML字符串，如果它接收到一个XML字符串，它会输出一个JavaScript对象。 | Examples |
| rbe | 按异常报告。  只有当其输入与前一个输入（字符串或数字）不同时，或者如果输入以可配置的量（死区模式）改变，则仅产生数字。| Example 3.4 |

## 社交节点

 基本的社交媒体节点支持与电子邮件和Twitter的交互。 它们使流可以发送或接收电子邮件，或发送或接收推文。

| 节点名称 | 简述 | 样例 |
| --- | --- | --- |
| email in | 可以配置为从IMAP服务器重复读取返回新的电子邮件。  将msg.topic设置为电子邮件主题，如果电子邮件为HTML，则将msg.payload设置为发送电子邮件文本正文或msg.html。 | Example |
| twitter in | 返回推文作为消息。  可用于搜索公众或用户的流，其中包含特定用户所配置的搜索字词或所有推文或由经过身份验证的用户收到的直接消息的推文。 | Example 1.1 |
| email out | 通过配置的IMAP服务器将传入的消息作为电子邮件发送。  主题和收件人全部可配置。  将二进制数据转换为附件。 | Example 1.2 |
| twitter out | 推荐配置的帐户上的msg.payload。  可以发送直接消息，并将作为图像发送二进制数据。 | Example 2.2 |

## 储存节点

 由于针对的是Raspberry Pi等设备，因此存储的默认节点设置非常有限，专注于基于文件的存储。

![http://noderedguide.com/wp-content/uploads/2015/10/Node-RED-Lecture-4-A-tour-of-the-core-nodes-42.jpg](file:////Users/bing/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image002.png)

图4.2默认存储，分析，高级和Raspberry Pi节点。

您应该注意，FRED，因为它是一个云服务，不支持基本的文件节点。 而是用Mongo到Dropbox的各种存储节点替代这些。 但是，为了完整，默认节点在这里被覆盖，以便您可以使用它们，如果您自己安装Node-RED的话（参见第7讲）。

| 节点名称 | 简述 | 样例 |
| --- | --- | --- |
| tail| 尾部（即要添加的东西的手表）到配置的文件。  （仅适用于Linux / Mac）这将不适用于Windows文件系统，因为它依赖于tail -F命令。 | Examples |
| file in | 读取指定的文件并发送内容为msg.payload，文件名为msg.filename。可以在节点中配置文件名。  如果留空，则应在传入消息中设置msg.filename。 | Examples |
| file | 将msg.payload写入指定的文件，例如  创建日志。  可以在节点中配置文件名。  如果留空，则应在传入消息中设置msg.filename。  默认行为是附加到文件。  这可以改变为每次覆盖文件; 例如，如果要输出“静态”网页或报告。| Examples |

## 分析节点

 分析节点对传入的消息执行标准分析。 在默认节点集中，唯一提供的节点是情绪节点，可用于根据消息中使用的单词（例如电子邮件或推文）来尝试确定传入消息的情绪。

| 节点名称 | 简述 | 样例 |
| --- | --- | --- |
| sentiment | 情绪节点分析了msg.payload，并根据字分析对消息的情绪进行了评分。  它添加了一个msg.sentiment对象，其中包含生成的AFINN-111情绪分数为msg.sentiment.score。  分数通常在-5到+5之间。 | Example 5.5 |

## 高级节点

 一组提供各种功能的杂项节点。

| 节点名称 | 简述 | 样例 |
| --- | --- | --- |
| watch | 观看目录或文件进行更改。  您可以输入逗号分隔的目录和/或文件的列表。  你需要在包含空格的地方放置引号“...”。  在Windows上，必须在所有目录名中使用双反斜杠\\。实际更改的文件的完整文件名将放入msg.payload，而在msg.topic中返回监视列表的字符串版本。msg.file只包含被更改的文件的短文件名。 msg.type的类型更改，通常是文件或目录，而msg.size保存文件大小（以字节为单位）。| Examples |
| feedparse | 该节点监视RSS / atom feed的新条目，并将新条目作为消息传递。  它可以被配置为以特定间隔查询馈送。 | Examples |
| exec | 调用一个系统命令，并提供3个输出：stdout，stderr和返回码。  默认情况下，使用调用命令的exec（）在等待完成时阻塞，然后一次返回完整的结果以及任何错误。 | Examples |

## Raspberry Pi 节点

| 节点名称 | 简述 | 样例 |
| --- | --- | --- |
| rpi_gpio in | 树莓Pi输入节点。  根据输入引脚的状态，产生一个0或1的msg.payload。  您也可以使能输入上拉电阻或下拉电阻。msg.topic设置为pi / {引脚号} 需要RPi.GPIO python库版本0.5.8（或更好）为了工作。注意：我们正在使用连接器P1上的实际物理引脚号，因为它们更容易定位。| Examples lecture 7 |
| rpi_gpio out | Raspberry Pi输出节点。  预期使用0或1（或true或false）的msg.payload。  将选定的物理引脚设置为高电平或低电平，具体取决于传递的值。引脚在部署时的初始值也可设置为0或1.当使用PWM模式时，需要输入值为0 - 100。需要RPi.GPIO Python库版本0.5.8（或更好）才能工作。| Examples 1.1, lecture 7 |
| rpi_mouse | Raspberry Pi鼠标按钮节点。  当选择的鼠标按钮被按下并释放时，生成1或0的msg.payload。  还将msg.button设置为代码值，1 = left，2 = right，4 = middle，因此您可以计算出按下哪个按钮或组合 | Examples lecture 7 |


## 总结：

在本讲座中，您将看到安装时可用的默认Node-RED节点的摘要，以及FRED添加的扩展节点集。 正如你所看到的，有各种各样的节点允许您构建很少或没有编程的复杂流。

您也看到并不是所有的节点总是可用的，例如，除了在Pi上实际运行Node-RED之外，Raspberry Pi节点不起作用。 所以它总是用于检查您是否可以运行在您环境中的节点。

然而，考虑到可用的大量节点，以及社区每天创建新节点的事实，您可能会找到一个满足您需求的节点。 如果没有，您可以回到灵活的功能节点，甚至创建自己的节点，这一块将在高级讲座中讨论。


