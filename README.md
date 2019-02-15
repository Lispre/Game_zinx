# Game_zinx
这个软件包含一个服务器框架和一个在线游戏的demo

## 目录布局
zinx目录是框架本身

customer目录用来放置业务实现，当前放置了一个游戏服务器的demo

## 依赖
1. libprotoc 3.6.1
2. cmake version 3.13.2

## 编译
```
mkdir build
cd build
cmake ../
make
make install
```

## 框架简介
zinx框架是用来处理通用IO，协议和事件的。
框架包含以下类：
+ server类
> 框架包含一个server类的单例对象，所有IO和数据处理的业务都应该依附于该对象。
+ Amessage类
> 这是一个抽象类，负责封装业务相关的数据。***开发者应该继承该类实现自定义的各种消息类型。***
+ Achannel类
> 这是一个抽象类，负责处理文件层面的数据IO。其中大部分方法都是基于linux的系统调用实现。类实例应该按需安装(install)或卸载(uninstall)。***开发者应该继承该类并重写部分方法，实现原始数据收发功能***
+ Aprotocol类
> 这是一个抽象类，负责将Achannel对象收发的原始数据和Amessage对象之间进行转换。每个Achannel对象可以绑定最多一(0~1)个Aprotocol对象。***开发者应该继承该类并重写部分方法，实现通信协议功能***
+ Arole类
> 这是一个抽象类，可以绑定最多一个Achannel对象作为输出通道。该类负责处理收到的各类Amessage对象，或产生并发送Amessage对象。***开发者应该核心的业务处理在该类的派生类中实现***
+ Request结构和Response结构
> 这两个结构体的布局完全相同只是成员变量名称不同。用来将Amessage对象和处理它的Arole或发送它的Arole封装起来。***开发者只需按照C语言的风格使用这个结构体，不要去无谓的继承该结构体***

## 举例
