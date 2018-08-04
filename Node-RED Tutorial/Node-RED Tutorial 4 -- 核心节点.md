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

| 
节点名称

 | 

简述

 | 

样例

 |
| 

sentiment

 | 

情绪节点分析了msg.payload，并根据字分析对消息的情绪进行了评分。  它添加了一个msg.sentiment对象，其中包含生成的AFINN-111情绪分数为msg.sentiment.score。  分数通常在-5到+5之间。

 | 

Example 5.5

 |

## 高级节点

 一组提供各种功能的杂项节点。

| 
节点名称

 | 

简述

 | 

样例

 |
| 

watch

 | 

观看目录或文件进行更改。  您可以输入逗号分隔的目录和/或文件的列表。  你需要在包含空格的地方放置引号“...”。  在Windows上，必须在所有目录名中使用双反斜杠\\。

实际更改的文件的完整文件名将放入msg.payload，而在msg.topic中返回监视列表的字符串版本。msg.file只包含被更改的文件的短文件名。 msg.type的类型更改，通常是文件或目录，而msg.size保存文件大小（以字节为单位）。

 | 

Examples

 |
| 

feedparse

 | 

该节点监视RSS / atom feed的新条目，并将新条目作为消息传递。  它可以被配置为以特定间隔查询馈送。

 | 

Examples

 |
| 

exec

 | 

调用一个系统命令，并提供3个输出：stdout，stderr和返回码。  默认情况下，使用调用命令的exec（）在等待完成时阻塞，然后一次返回完整的结果以及任何错误。

 | 

Examples

 |

## Raspberry Pi 节点

| 
节点名称

 | 

简述

 | 

样例

 |
| 

rpi_gpio in

 | 

树莓Pi输入节点。  根据输入引脚的状态，产生一个0或1的msg.payload。  您也可以使能输入上拉电阻或下拉电阻。

msg.topic设置为pi / {引脚号}

需要RPi.GPIO python库版本0.5.8（或更好）为了工作。

注意：我们正在使用连接器P1上的实际物理引脚号，因为它们更容易定位。

 | 

Examples lecture 7

 |
| 

rpi_gpio out

 | 

Raspberry Pi输出节点。  预期使用0或1（或true或false）的msg.payload。  将选定的物理引脚设置为高电平或低电平，具体取决于传递的值。引脚在部署时的初始值也可设置为0或1.当使用PWM模式时，需要输入值为0 - 100。

需要RPi.GPIO Python库版本0.5.8（或更好）才能工作。

 | 

Examples 1.1, lecture 7

 |
| 

rpi_mouse

 | 

Raspberry Pi鼠标按钮节点。  当选择的鼠标按钮被按下并释放时，生成1或0的msg.payload。  还将msg.button设置为代码值，1 = left，2 = right，4 = middle，因此您可以计算出按下哪个按钮或组合。

 | 

Examples lecture 7

 |

## 扩展FRED节点集

FRED服务向标准默认设置添加了许多节点。 已经添加了为FRED编写或从公共存储库中收集的这些新节点，因为它们提供了扩展了香草节点集的功能的有用功能。

注意：这些节点可以通过使用FRED安装面板安装在FRED中。 有关如何安装节点的快速示例，请查看本教程。

如您所见，这些附加节点中的大多数重点放在与FRED性质相符的服务和功能上，即基于云的服务。 在许多情况下，他们专注于使用Node-RED进行基于Web的集成或访问企业级服务。

![http://noderedguide.com/wp-content/uploads/2015/10/t_Node-RED-Lecture-4-A-tour-of-the-core-nodes-10.jpg](file:////Users/bing/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image003.jpg)

图4.3扩展FRED节点

## 扩展的社交媒体节点集

您可以看到，FRED服务增加了大量社交媒体节点，从Pushbullet到Slackbot到Instagram。

| 
节点名称 | 简述 | 样例 | 

---- | -- | --- |

pushbullet in

 | 

连接到流行的Pushbullet服务，并从所有连接的设备接收Pushbullet数据。  支持数据，链接和文件。

 | 

Examples

 |
| 

pushbullet out

 | 

允许您将Pushbullet消息发送到安装了Pushbullet应用程序的所有设备。

 | 

Examples

 |
| 

XMPP in

 | 

从XMPP即时消息服务器接收消息。  好友字段表示您收到的好友或房间。  存在信息在第二输出链路上传送。

 | 

Examples

 |
| 

XMPP out

 | 

发送消息到XMPP即时消息服务器。  使用主题发送到房间（渠道）并支持存在通知。

 | 

Examples

 |
| 

slack

 | 

一个通用节点，提供了一个简单的方式来发布在通过其webhook URL指定的松弛通道。  可以配置用户名，表情符号和支持附件。

 | 

Examples

 |
| 

slackbot in

 | 

一个使用您在Slack上创建的机器人的节点，并在Slack bot成为其中的任何通道中提供一个侦听器。  输出msg.payload作为传入消息。  并输出具有完整的Slack消息详细信息的msg.SlackObj。

 | 

Examples 5.7

 |
| 

slackbot out

 | 

使用您在Slack上创建的机器人的节点根据提供的Bot API令牌将msg.payload发送到Slack。  如果需要，您可以选择覆盖目标通道 \- 在编辑对话框中或通过设置msg.channel。

 | 

Examples 5.7

 |
| 

delicious

 | 

将书签保存到您的Delicious帐户的节点。  有效载荷应包含要保存的URL，而msg.title包含书签名称。  可以设置可选的描述字段。

 | 

Examples

 |
| 

pinboard

 | 

将书签保存到您的Pinboard帐户的节点。  有效载荷应包含要保存的URL，而msg.title包含书签名称。  可以设置可选的描述字段。

 | 

Examples

 |
| 

flickr

 | 

将照片保存到配置的Flickr帐户。 msg.payload需要具有图像的缓冲区，并且可以设置可选的标题，描述和标签属性。

 | 

Examples

 |
| 

foursquare

 | 

查询您的Foursquare帐户，以满足基于您所在位置的可配置要求的场所。  结果可以作为单个消息或可配置的一组消息传回。

 | 

Examples

 |
| 

swarm in

 | 

一个节点每四分钟轮询Foursquare风暴签到。  作为JSON对象返回。

 | 

Examples

 |
| 

swarm out

 | 

Swarm查询节点可用于通过身份验证的用户搜索所有Swarm签入。

 | 

Examples

 |
| 

instagram in

 | 

每15分钟查询一次配置的Instagram帐号，为每个消息传递一个新的照片，作为缓冲区对象或URL。

 | 

Examples

 |
| 

instagram

 | 

与节点中的Instagram相同，除了被传入消息触发。

 | 

Examples

 |

## 扩展的存储节点集

您可以看到，FRED服务增加了大量社交媒体节点，从Pushbullet到Slackbot到Instagram。

| 
节点名称

 | 

简述

 | 

样例

 |
| 

amazonS3 watch

 | 

Amazon S3查看节点。  查看文件事件。  默认情况下，会报告所有文件事件，但可以提供文件名模式以将事件限制为具有与glob模式匹配的完整文件名的文件。  事件消息由msg.payload属性中的完整文件名，msg.file中的文件名，msg.event中的事件类型组成。

 | 

Examples

 |
| 

amazonS3 in

 | 

Amazon S3输入节点。  从Amazon S3 bucket下载内容。  可以在节点桶属性或msg.bucket属性中指定桶名称。  要下载的文件的名称取自节点文件名属性或msg.filename属性。  下载的内容以msg.payload属性发送。  如果下载失败，msg.error将包含一个错误对象。

 | 

Examples

 |
| 

amazonS3 out

 | 

Amazon S3 输出节点。  将内容上传到Amazon S3存储区。  可以在节点桶属性或msg.bucket属性中指定桶名称。 Amazon S3上的文件名取自节点文件名属性或msg.filename属性。内容取自节点localFilename属性，msg.localFilename属性或msg.payload属性。

 | 

Examples

 |
| 

box watch

 | 

Box是Dropbox的企业版。  此节点在Box上监视文件事件。  默认情况下，报告所有文件事件，但可以提供文件名模式以将事件限制为具有与glob模式匹配的完整文件名的文件。  事件消息由msg.payload属性中的完整文件名，msg.file中的文件名，msg.event中的事件类型和msg.data中事件API返回的完整事件条目组成。

 | 

Examples

 |
| 

box in

 | 

Box输入节点。  从Box下载内容。 Box上的文件名取自节点文件名属性或msg.filename属性。  内容以msg.payload属性发送。

 | 

Examples

 |
| 

box out

 | 

Box输出节点。  将内容上传到Box。 Box上的文件名取自节点文件名属性或msg.filename属性。  内容取自节点localFilename属性，msg.localFilename属性或msg.payload属性。

 | 

Examples

 |
| 

dropbox watch

 | 

查看在Dropbox上的文件事件。

默认情况下，报告所有文件事件，但可以提供文件名模式以将事件限制为具有与glob模式匹配的完整文件名的文件。

事件消息由msg.payload属性中的完整文件名，msg.file中的文件名，msg.event中的事件类型和dropbox.js API PulledChange对象inmsg.data组成。

 | 

Examples

 |
| 

dropbox in

 | 

Dropbox输入节点。  从Dropbox下载内容。 Dropbox上的文件名取自节点文件名属性或msg.filename属性。  下载的内容以msg.payload属性发送。  如果下载失败，msg.error将包含一个错误对象。

 | 

Examples

 |
| 

dropbox out

 | 

Dropbox出节点。  将内容上传到Dropbox。

Dropbox上的文件名取自节点文件名属性或msg.filename属性。  您可以通过设置localFilename字段或msg.localFilename属性作为文件名传递内容，也可以使用msg.payload直接传递内容。The file will be uploaded to a directory on Dropbox called Apps/{appname}/{appfolder}, where {appname} and {appfolder} are set when you set up the Dropbox application key and token.

 | 

Examples

 |
| 

MongoDB in

 | 

根据所选运算符调用MongoDB收集方法。

根据.find（）函数，使用msg.payload作为查询语句查询集合。 Count使用msg.payload作为查询语句返回集合中的文档数或与查询匹配的计数。

聚合提供使用msg.payload作为流水线数组的聚合流水线的访问。

您可以在节点配置或msg.collection中设置收集方法。  在节点中设置它将覆盖msg.collection。

 | 

Examples

 |
| 

MongoDB out

 | 

一个简单的MongoDB输出节点。  可以从选定的集合中保存，插入，更新和删除对象。

保存将更新现有对象或插入新对象（如果尚不存在）。

插入将插入一个新对象。

更新将修改现有对象或对象。

删除将删除与在msg.payload上传递的查询相匹配的对象。  空白查询将删除集合中的所有对象。

 | 

Examples

 |
| 

mysql

 | 

允许对MySQL数据库进行基本访问。

此节点对配置的数据库使用查询操作。  这允许INSERTS和DELETES两者。 msg.topic必须保存对数据库的查询，结果以msg.payload返回。

返回的有效载荷通常将是结果行的数组。  如果没有找到密钥，则返回null。

 | 

Examples

 |
| 

postgres

 | 

PostgreSql I / O节点。

使用msg.queryParameters中的可选查询参数执行msg.payload中指定的查询。  查询中的queryParameters必须指定为$ propertyname。

当从查询中接收数据时，输出上的msg.payload将是返回记录的JSON数组。

 | 

Examples

 |

## Node RED 中物联网节点

| 
IoT平台节点

 |
| 

wotkit in

 | 

WoTKit传感器输入节点，用于从WoTKit传感器检索新数据。  每当在WoTKit IoT平台中的传感器上接收到新数据时，节点就会生成消息。 message.payload包含传感器字段名称与传感器值的映射。  该节点配置了WoTKit用户凭据。  传感器名称应为{username}。{sensorname}，或者您可以使用数字传感器ID。

 | 

Examples

 |
| 

wotkit out

 | 

WoTKit输出节点向注册的WoTKit传感器发送数据。  该节点将使用message.payload创建一个数据对象。

message.payload必须包含与传感器字段匹配的键值对的对象。  节点配置有WoTKit用户凭据。传感器名称应为{username}。{sensorname}，或者您可以使用数字传感器ID。

 | 

Examples

 |
| 

wotkit data

 | 

WoTKit历史数据节点，它可以通过任意数量的元素或在请求之前的相对时间从WoTKit传感器中检索历史数据。 message.payload包含传感器字段名称与传感器值的映射。  传感器名称应为{username}。{sensorname}，或者您可以使用数字传感器ID。

 | 

Examples

 |
| 

wotkit control out

 | 

WoTKit控制输出节点能够将事件发送到注册的WoTKit传感器/执行器的控制通道。  该节点将使用message.payload对象来创建一个控件事件。 message.payload必须包含每个消息的键值对的对象。  传感器名称应为{username}。{sensorname}，或者您可以使用数字传感器ID。

 | 

Examples

 |
| 

wotkit control input

 | 

WoTKit控制输入节点可访问注册的WoTKit传感器/执行器的控制通道。  当WoTKit传感器接收到控制事件时，该节点将创建一个包含该事件的message.payload对象。  传感器名称应为{username}。{sensorname}，或者您可以使用数字传感器ID。

 | 

Examples

 |
| 

dweetio in

 | 

侦听来自Dweet.io的消息

Thing ID应该是全球唯一的，因为它们都是公开的。  建议您使用GUID。 Thing ID设置为msg.dweet，将TimeStamp设置为msg.created。

 | 

Examples

 |
| 

dweetio out

 | 

发送msg.payload到dweet.io

（可选）使用msg.thing设置Thing ID，如果尚未在属性中设置。

您需要使独一无二的Thing ID - 建议您使用GUID。

 | 

Examples

 |

## 扩展的分析节点集

FRED平台仅添加有限数量的分析节点，因为默认设置相当广泛。

| 
节点名称

 | 

简述

 | 

样例

 |
| 

smooth

 | 

一个简单但灵活的节点，可以跨多个先前的值提供各种功能，包括最大值，最小值，平均值，高通和低通滤波器。  仅适用于数字，如果无法将输入转换为数字，则会失败。

 | 

Examples

 |
| 

wordpos

 | 

分析msg.payload并对每个单词的词性进行分类，将msg.pos返回为名词，动词，形容词，副词等的数组。

 | 

Examples

 |

## Google节点

FRED支持多个Google节点与一系列Google服务进行互动。

| 
节点名称

 | 

简述

 | 

样例

 |
| 

Google plus

 | 

与Google+ API进行交互，以获取有关人员，活动和评论的信息。

人物 \- 允许您与Google+个人资料进行互动。  您可以获得特定的个人资料，搜索个人资料，或收集+1的人员列表，或转发一项活动。

活动 \- 让您与Google+活动进行互动。  您可以获得特定活动，搜索活动或收集与个人直接相关的活动列表。

评论 \- 允许您与Google+评论进行互动。  您可以获得特定的评论，或收集附加到活动的评论列表。

 | 

Examples

 |
| 

googleplaces

 | 

一个高度灵活的节点，利用Google Places API来查找和了解有关本地企业的更多信息。  搜索可以基于排名，半径，价格，关键字，语言等。

 | 

Examples

 |
| 

Google calendar in

 | 

观看日历并在日历中的事件之前，之中或之后返回消息的节点。  可配置为准确地设置消息生成的时间。

 | 

Examples

 |
| 

Google calendar out

 | 

在Google日历中创建一个条目：

有效负载 \- 使用快速添加格式描述事件的字符串或表示插入请求的请求体的对象

日历 \- 添加事件的日历（可选，默认为节点日历属性或用户的主日历）

sendNotifications - 一个布尔值，用于确定是否应将通知发送给与会者（可选，默认为false）

 | 

Examples

 |

## 健身节点

FRED健身节点覆盖了许多受欢迎的健身器材。

| 
节点名称

 | 

简述

 | 

样例

 |
| 

strava

 | 

在Strava上获取最新的活动。

该节点在收到消息时，会返回已验证用户帐户中的最新活动。  返回可用的活动，位置和时间。

 | 

Examples

 |
| 

Fitbit in

 | 

定期为新数据查看Fitbit。  生成的消息由nodetype属性（目标，睡眠或徽章）决定。

 | 

Examples

 |
| 

Fitbit activities

 | 

从Fitbit检索用户数据，并返回由nodetype属性（作为fitbit）确定的msg.payload。

可以将msg.date属性设置为ISO 8601格式日期（例如2014-09-25）以检索活动和睡眠日志的历史数据。  如果没有提供日期，则将检索今天的数据。  在睡眠的情况下，这是前一次睡眠的数据。

 | 

Examples

 |
| 

jawbone

 | 

Jawbone Up节点可用于检索自提供的时间（以Epoch为单位）完成的训练。  这一次可以作为节点上的设置或消息输入的msg.starttime部分传递。  节点上设置的值优先于传入消息的内容。

 | 

Examples

 |

## 天气节点

FRED添加了一组节点以访问各种天气服务。

| 
节点名称

 | 

简述

 | 

样例

 |
| 

openweathermap

 | 

查询openweathermap.com网站的节点，以查看城市/国家/地区/拉夫/长对对应的天气信息。  存在两个节点：一个是UI配置的，一个可以接受配置信息作为输入消息。

 | 

Examples

 |
| 

forecastio

 | 

用于查询Forecastio.com网站的节点，以查看纬度/长度对的天气信息。  存在两个节点：一个是UI配置的，一个可以接受配置信息作为输入消息。

 | 

Examples

 |
| 

wunderground

 | 

一个节点，定期查询Weather Underground API的当前天气数据，并在检测到更改时返回。  存在两个节点：一个是UI配置的，一个可以接受配置信息作为输入消息。

 | 

Examples

 |

## Salesforce节点

FRED提供了一组实验性的SalesForce节点。

| 
节点名称

 | 

简述

 | 

样例

 |
| 

salesforce

 | 

一组与流行的salesforce.com服务交互的5个节点。  节点可以生成SOSL查询，DML语句，订阅salesforce流API或解析出站的Salesforce消息对象。

 | 

Examples

 |

## 交通节点

| 
节点名称

 | 

简述

 | 

样例

 |
| 

TfL bus

 | 

为伦敦（英国）公共汽车和河流公交车提供现场巴士出发/到达信息。

该节点使得用户可以获得到达所选停靠点的所选线路的总线或河流总线到达信息。  节点返回第一个车辆/船只到达特定的停靠点。  数据由伦敦交通局提供。

 | 

Examples

 |
| 

TfL underground

 | 

获得伦敦地铁的地下线状态的节点。  它返回指定行的各种状态信息，包括总体状态，中断信息等

 | 

Examples

 |

## 格式化节点

| 
节点名称

 | 

简述

 | 

样例

 |
| 

moment

 | 

时刻是一个日期/时间格式化器节点，它将一个JS datetime对象或一个可以解析的字符串作为输入。  如果输入为空，则不存在或为空字符串，则将使用当前日期/时间。  这可以很容易地将当前时间戳添加到任何类型的流中。

输出是格式化的字符串或日期对象onmsg.payload默认情况下，通过设置输出字段进行更改。

 | 

Examples

 |

## 总结：

在本讲座中，您将看到安装时可用的默认Node-RED节点的摘要，以及FRED添加的扩展节点集。 正如你所看到的，有各种各样的节点允许您构建很少或没有编程的复杂流。

您也看到并不是所有的节点总是可用的，例如，除了在Pi上实际运行Node-RED之外，Raspberry Pi节点不起作用。 所以它总是用于检查您是否可以运行在您环境中的节点。

然而，考虑到可用的大量节点，以及社区每天创建新节点的事实，您可能会找到一个满足您需求的节点。 如果没有，您可以回到灵活的功能节点，甚至创建自己的节点，这一块将在高级讲座中讨论。


