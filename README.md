# flamingo
一款高性能、轻量级的即时通讯软件
目前即时通讯软件实现了如下功能（这里只列举网络相关的功能，其他客户端已经实现的功能不统计在列，请自行发现）：
注册
登录
查找好友、查找群
添加好友、添加群
好友列表、群列表、最近会话
单人聊天功能（包括发文字、表情、窗口抖动、离线文件）
群组功能（包括发文字、表情）
群发消息
修改密码
修改个人信息（自定义昵称、签名、个性头像等个人信息）
自动升级功能
	
客户端还有很多细节功能，比如头像有三种显示模式、好友上线动画、聊天记录、聊天自动回复功能等，有兴趣的同学可以自己探索尝试一下吧，这里就不截图了。
下面介绍一下服务器代码和pc客户端代码的编译与运行环境：
flamingo服务器端代码使用cmake + makefile编译，使用了纯C++11开发，运行于linux系统下（我的系统是CentOS7.0），为了支持C++11，你的gcc版本至少要大于4.7，我的版本是4.8.5。另外，使用了数据库，我的数据库版本是5.7.17。服务器代码不仅是一款即时通讯软件的服务器代码，同时也是一款通用的C++11服务器框架。
服务器代码使用方法：
编译方法：
1. 进入程序目录，输入cmake . (注意有一个点号，表示当前目录)
2. 没有错误，输入make
3.最终会产生三个可执行程序，mychatserver、myfilesever和myimgserver。编译完成
部署方法：
简单说明：mysql数据库的用户名为root，密码为空，请根据你自己的需要设置相应的用户名和密码（目前写死在程序中）。mychatserver是聊天服务器，myfileserver是文件服务器，文件服务器负责上传和下载聊天中发送的文件，myimgserver负责上传和下载聊天中的图片。三个服务相互独立，互不影响。聊天服务器监听端口是20000，文件服务器端口是20001，图片服务器端口号是20002，这三个端口供客户端连接，其中聊天端口和客户端是长连接，文件端口和图片可选择长连接或短连接。
       第一次运行mychatserver时，如果能顺利连上mysql，mychatserver会自动检测是否存在名为myim的数据库，如果不存在则创建，并新建三张信息表，分别是用户信息表：t_user, 好友关系表t_user_relationship和聊天消息记录表t_chatmsg。第一次启动文件服务器时会创建filecache目录，这个目录用来存储聊天中的聊天图片和离线文件以及客户端升级包。
    为了方便查看代码，我用Visual Studio来管理代码，可使用VS打开myserver.sln查看和管理代码。（VS版本必须是VS2013或以上版本）
客户端代码使用方法：
编译：
1.用VS2013打开程序目录下的：Flamingo.sln，你可以使用其他的VS版本，但是至少不低于VS2013，因为客户端代码也使用了大量C++11语法和库，VS2013及以上版本才能较好的支持C++11的语法。
2. 打开的解决方案包括三个项目：Flamingo是即时通讯主程序，CatchScreen是聊天中使用的截图工具，iUpdateAuto是升级功能中用到的解压工具。
3. 用VS2013编译整个解决方法即可，编译成功以后将在Bin目录下生成对应的程序。启动Flamingo.exe注册一个账号就可以开始使用flamingo了。

    如果你暂时不想研究服务器代码，但又想使用客户端，你可以连接我的测试服务器，测试服务器地址是：
聊天服务器地址：120.55.94.78 端口号：20000
文件服务器地址：120.55.94.78 端口号：20001
图片服务器地址：120.55.94.78 端口号：20002
你可以在登录界面的网络设置里面进行设置（登录界面右上角最小化按钮左边的一个按钮）。

详情参见： http://blog.csdn.net/analogous_love/article/details/69481542

    如果有您对我的程序有任何意见或者建议，或者有不错的想法欢迎与我交流或者给我留言（QQ：906106643）.。代码中也有些“拿来主义”，另外程序中使用的图片和图标来源于网络，仅供用于学习，请勿用于商业用途，如果不小心侵犯了您的版权，请联系我。
        
        
