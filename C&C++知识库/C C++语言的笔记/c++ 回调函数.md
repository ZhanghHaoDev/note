# C++ 回调函数

生命周期管理：

确保回调函数在调用时仍然有效，避免悬挂指针。
使用智能指针（如 std::shared_ptr）管理回调函数对象的生命周期。
线程安全：

在多线程环境中使用回调函数时，确保线程安全。
使用互斥锁（如 std::mutex）保护共享数据。
参数传递：

回调函数通常接受特定的参数，这些参数由调用者传递。
确保参数类型和数量与回调函数签名匹配。
错误处理：

处理回调函数中的异常，避免未捕获的异常导致程序崩溃。
使用 try-catch 块捕获并处理异常。
性能考虑：

回调函数的调用频率可能很高，确保回调函数的执行效率。
避免在回调函数中进行耗时操作。
示例应用：

GUI编程：按钮点击事件处理。
网络编程：数据接收完成通知。
多线程编程：线程完成通知。

## 1. 简介

回调函数是通过函数指针或函数对象传递给另一个函数的函数，当特定事件发生时由该函数调用。

## 2. 用途

用于事件驱动编程，如GUI事件处理、网络请求完成、数据处理等。
用于异步操作，如异步I/O、线程完成通知等。

### 回调函数的应用

- **图形用户界面**：处理用户交互事件，如按钮点击。
- **网络编程**：处理网络请求的响应。
- **定时器**：在特定时间后执行某些操作。

## 3. 实现的方式

函数指针：最基本的回调实现方式。
函数对象（仿函数）：通过重载 operator() 实现。
Lambda表达式：C++11引入的简洁回调方式。
std::function：C++11引入的通用回调机制，支持函数指针、函数对象和Lambda。

**实例**

下面是一个使用 C++ 标准库中的 `std::function` 来实现回调函数的简单示例：

```cpp
#include <iostream>
#include <functional>

// 定义一个函数，它接受一个回调函数作为参数
void process_data(std::function<void(int)> callback) {
    for (int i = 0; i < 5; ++i) {
        // 在适当的时候调用回调函数
        callback(i);
    }
}

int main() {
    // 定义一个回调函数
    auto callback = [](int data) {
        std::cout << "Processing data: " << data << std::endl;
    };

    // 将回调函数作为参数传递给 process_data 函数
    process_data(callback);

    return 0;
}
```

### 执行顺序解析

1. **main 函数开始执行**：程序的入口点。
2. **定义回调函数**：在 main 函数中定义了一个匿名函数（lambda 表达式），该函数接受一个整数参数并打印出来。
3. **调用 process_data 函数**：将定义的回调函数作为参数传递给 `process_data` 函数。
4. **process_data 函数执行**：开始循环，每次循环调用传入的回调函数。
5. **回调函数被调用**：在每次迭代中，回调函数被调用，并打印出当前处理的数据。
6. **process_data 函数结束**：处理完所有数据后，函数返回到 main 函数。
7. **main 函数结束执行**：程序执行完毕。

### 回调函数的应用

在实际的应用程序中，回调函数可以用于多种场景，例如：

- **图形用户界面**：处理用户交互事件，如按钮点击。
- **网络编程**：处理网络请求的响应。
- **定时器**：在特定时间后执行某些操作。

## 回调函数的执行和获取数据

在开发摄像头的时候，获取摄像头数据的方式都是使用回调函数的机制

1. 为什么使用回调函数
    + **异步处理**：摄像头数据的获取通常是一个异步过程，使用回调函数可以在数据准备好时立即通知应用程序，而不需要阻塞主线程等待数据。
    + **解耦代码**：回调函数可以将数据获取逻辑与数据处理逻辑分离，使代码更加模块化和易于维护。
    + **提高响应速度**：通过回调函数，应用程序可以在数据到达时立即处理，提高了响应速度和用户体验。
    + **灵活性**：回调函数允许开发者定义自己的数据处理逻辑，可以根据不同的需求灵活处理摄像头数据。

2. 回调函数的执行流程
从main函数开始，调用注册回调函数的接口，注册回调函数，这个时候，如果注册函数在main函数当中，那么需要一个暂停的操作，比如暂停五秒，在暂停的时候，回调函数开始执行，开始获取摄像头的数据。五秒之后，main函数就继续执行暂停五秒之后的代码

**问题：如何获取回调函数的数据**

在开发摄像头的时候，遇到的一个问题是：摄像头的数据是通过回调函数获取的，但是，回调函数的执行机制是在mian函数之后，并且回调函数当中获取的数据也传递不出来，如何解决？

这里提供了一个解决办法：

具体的操作是：定义全局变量

```cpp
// 全局变量 video_data.h
#ifndef VIDEO_DATA_H
#define VIDEO_DATA_H

#include <vector>
#include <mutex>

extern std::vector<char> globalBuffer;
extern std::mutex bufferMutex;

#endif // VIDEO_DATA_H

// 全局变量 video_data.cpp
#include "video_data.h"

// 定义全局变量
std::vector<char> globalBuffer;
std::mutex bufferMutex;

// 海康威视摄像头的具体代码
// 注册函数
int video_sensor::register_callback() {
    int errorCode = 0;
    if (userID < 0) {
        std::cerr << "未登录设备，文件: " << __FILE__ << ", 行号: " << __LINE__ << std::endl;
        return -1;
    }

    NET_DVR_PREVIEWINFO struPlayInfo = {0};
    struPlayInfo.lChannel = 1; // 预览通道号
    struPlayInfo.dwStreamType = 0; // 主码流
    struPlayInfo.dwLinkMode = 0; // TCP方式
    struPlayInfo.bBlocked = 1; // 阻塞取流

    LONG lRealPlayHandle = NET_DVR_RealPlay_V40(userID, &struPlayInfo, g_RealDataCallBack_V30, this);
    errorCode = NET_DVR_GetLastError();

    if (errorCode != 0) {
        std::cerr << "获取视频流失败，错误码: " << errorCode << "，文件: " << __FILE__ << ", 行号: " << __LINE__ << std::endl;
        return lRealPlayHandle;
    }

    return 0;
}

// 回调函数
void video_sensor::g_RealDataCallBack_V30(LONG lRealHandle, DWORD dwDataType, BYTE* pBuffer, DWORD dwBufSize, void* dwUser) {
	switch (dwDataType) {
	case NET_DVR_SYSHEAD: //系统头
		if (lPort >= 0) {
			break;  //该通道取流之前已经获取到句柄，后续接口不需要再调用
		}
		if (!PlayM4_GetPort(&lPort)) {
			break;
		}
		if (dwBufSize > 0) {
			if (!PlayM4_SetStreamOpenMode(lPort, STREAME_REALTIME)) {   //设置实时流播放模式
				break;
			}
			if (!PlayM4_OpenStream(lPort, pBuffer, dwBufSize, 1024 * 1024)) {  //打开流接口
				break;
			}
			if (!PlayM4_Play(lPort, NULL)) { //播放开始
				break;
			}
		}
		break;
	case NET_DVR_STREAMDATA:
		if (dwBufSize > 0 && lPort != -1) {
			if (!PlayM4_InputData(lPort, pBuffer, dwBufSize)) {
				break;
			}
            // 将数据存储在全局变量中
            std::lock_guard<std::mutex> lock(bufferMutex);
            globalBuffer.insert(globalBuffer.end(), pBuffer, pBuffer + dwBufSize);
		}
		break;
	default: //其他数据
		if (dwBufSize > 0 && lPort != -1) {
			if (!PlayM4_InputData(lPort, pBuffer, dwBufSize)) {
				break;
			}
		}
		break;
	}
}

// main函数，具体的测试
#include <iostream>
#include <thread>
#include <chrono>
#include <fstream>
#include <cstring>
#include <ctime>

#include "video_sensor.h"
#include "video_data.h"

/*
* 图像传感器-采集音视频数据测试
* 测试结果：
* 采集成功：返回0，数据写入文件，可以正常播放
* 登录失败：返回负数，或者错误码
*/
int main(int argc, char *argv[]) {
    int error = 0;
    
    video_sensor video;
    if((error = video.login("admin", "aithu5656", "192.168.1.65")) != 0){
        std::cerr << "登录设备失败，错误码：" << error << std::endl;
        return error; 
    }

    video.register_callback();

    // 采集时长
    std::this_thread::sleep_for(std::chrono::seconds(10));

    // 访问全局变量中的数据
    {
        std::lock_guard<std::mutex> lock(bufferMutex);
        std::cout << "Received data size: " << globalBuffer.size() << " bytes" << std::endl;

        // 将数据写入文件
        std::ofstream outfile("output.mpg", std::ios::app | std::ios::binary);
        if (!outfile.is_open()) {
            std::cerr << "无法打开文件进行写入。" << std::endl;
            return 1;
        }

        outfile.write(reinterpret_cast<const char*>(globalBuffer.data()), globalBuffer.size());
        if (outfile.fail()) {
            std::cerr << "写入文件失败。" << std::endl;
            return 1;
        }

        outfile.close();
        if (outfile.fail()) {
            std::cerr << "关闭文件失败。" << std::endl;
            return 1;
        }
        std::cout << "数据已成功写入文件。" << std::endl;
    }

    return 0;
}

```

