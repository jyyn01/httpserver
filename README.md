## 项目简介

httpserver项目使用Linux网络编程知识，在Linux环境下使用C++搭建的web服务器，服务器能够支持相对数量的客户端访问，在这个项目中服务器支持客户端访问服务器中的图片、音视频等资源



## 项目主要功能



**接受客户端请求**：对浏览器的请求进行处理，解析HTTP报文

**组织http相应报文**：对客户端的请求，根据解析后的报文回复报文



## 反应堆架构



![](file://C:\Users\JP\AppData\Roaming\Typora\typora-user-images\image-20240207160142338.png?lastModify=1709132213)

在tcpserver类中，包含主反应堆和线程池和监听结构体，线程池中包含子线程指针（所有子线程），启动tcpserver会启动线程池就是把每个子线程创建出来在，可能需要一些时间需要阻塞主线程原因上面说到了，创建出来的线程执行函数，就是初始化反应堆并运行，反应堆干的事在while循环调用1.epoll_wait()得到触发事件的文件描述符（断开连接，读事件，写事件）对触发了事件的文件描述符通过fd和channelmap找到对应的channel调用里面的读回调写回调,2.在while循环里处理任务队列，在第另一个while循环处理任务队列，就是对channel（文件描述符）的增删改，并修改对应的channelmap，到此线程池的启动就完成了，上面说的是线程池的功能，但是创建出来还没有任务，接下来把得到的监听描述符封装成channel由主反应堆添加到任务队列，启动主反应堆（也是和上面一样循环处理）。



## 项目架构



![](C:\Users\JP\AppData\Roaming\Typora\typora-user-images\image-20240228225543093.png)

## 使用方法





**服务发启动**

填写对应的端口号和文件路径

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include "TcpServer.h"

int main(int argc, char* argv[])
{
#if 0
    if (argc < 3)
    {
        printf("./a.out port path\n");
        return -1;
    }
    unsigned short port = atoi(argv[1]);
    // 切换服务器的工作路径
    chdir(argv[2]);
#else
    unsigned short port = 10000;
    chdir("/home/robin/luffy");
#endif
    // 启动服务器
    TcpServer* server = new TcpServer(port, 4);
    server->run();

    return 0;
}
```

