# 第三章 SDL库的学习

# 1. SDL库的简介

官网：https://www.libsdl.org

文档：http://wiki.libsdl.org/SDL2/Introduction

SDL（Simple DirectMedia Layer）是一套开放源代码 的跨平台多媒体开发库，使用C语言写成。SDL提供 了数种控制图像、声音、输出入的函数，让开发者只要用相同或是相似的代码就可以开发出跨多个平台 （Linux、Windows、Mac OS X等）的应用软件。目前SDL多用于开发游戏、模拟器、媒体播放器等多媒 体应用领域。

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320173337-6d837ac4-1e36-437d-9aa7-68da9e5fe468.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320173337-6d837ac4-1e36-437d-9aa7-68da9e5fe468.png)

# 1.1. 环境的搭建

Windows：https://github.com/libsdl-org/SDL

Linux：sudo apt-get install libsdl2-dev

macOS：sudo apt-get install libsdl2-dev

# 1.2. SDL子系统

SDL将功能分成下列数个子系统

1. SDL_INIT_TIMER：定时器
2. SDL_INIT_AUDIO：音频
3. SDL_INIT_VIDEO：视频
4. SDL_INIT_JOYSTICK：摇杆
5. SDL_INIT_HAPTIC：触摸屏
6. SDL_INIT_GAMECONTROLLER：游戏控制器
7. SDL_INIT_EVENTS：事件
8. SDL_INIT_EVERYTHING：包含上述所有选项

# 2. SDL windows显示

# 2.1. 视频显示函数简介

1. SDL_Init()：初始化SDL系统
2. SDL_CreateWindow()：创建窗口SDL_Window
3. SDL_CreateRenderer()：创建渲染器SDL_Renderer
4. SDL_CreateTexture()：创建纹理SDL_Texture
5. SDL_UpdateTexture()：设置纹理的数据
6. SDL_RenderCopy()：将纹理的数据拷贝给渲染器
7. SDL_RenderPresent()：显示
8. SDL_Delay()：工具函数，用于延时
9. SDL_Quit()：退出SDL系统

# 2.2. 数据结构简介

1. SDL_Window 代表了一个“窗口”
2. SDL_Renderer 代表了一个“渲染器”
3. SDL_Texture 代表了一个“纹理”
4. SDL_Rect 一个简单的矩形结构

存储RGB和存储纹理的区别： 比如一个从左到右由红色渐变到蓝色的矩形，用存储RGB的话就需要把矩形中每个点的具体颜色值存储下来；而纹理只是一些描述信息，比如记录了矩形的大小、起始颜色、终止颜色等信息，显卡可以通过这些信息推算出矩形块的详细信息。 所以相对于存储RGB而已，存储纹理占用的内存要少的多。

# 2.3. code - demo

```rust
// Windows 显示 demo
// 用户关闭窗口或按下任意键时退出。
#include <SDL.h>
#include <iostream>

int main(int argc, char* argv[]) {
    SDL_Init(SDL_INIT_VIDEO);

    SDL_Window* window = SDL_CreateWindow("SDL Window Demo", SDL_WINDOWPOS_UNDEFINED, SDL_WINDOWPOS_UNDEFINED, 640, 480, 0);
    if (window == NULL) {
        std::cout << "Could not create window: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_Renderer* renderer = SDL_CreateRenderer(window, -1, 0);
    if (renderer == NULL) {
        std::cout << "Could not create renderer: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_SetRenderDrawColor(renderer, 255, 0, 0, 255);
    SDL_RenderClear(renderer);
    SDL_RenderPresent(renderer);

    SDL_Event event;
    bool running = true;
    while (running) {
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT) {
                running = false;
            }
            if (event.type == SDL_KEYDOWN) {
                running = false;
            }
        }
    }

    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();

    return 0;
}
```

# 3. SDL 事件

# 3.1. SDL 事件函数

1. SDL_WaitEvent()：等待一个事件
2. SDL_PushEvent()：发送一个事件
3. SDL_PumpEvents()：将硬件设备产生的事件放入事件队列，用于读取事件，在调用该函数之前，必须调用SDL_PumpEvents搜集键盘等事件
4. SDL_PeepEvents()：从事件队列提取一个事件

# 3.2. SDL 事件 数据结构

SDL_Event 代表一个事件

# 3.3. code

用户关闭窗口或按下任意键时退出

```rust
#include <SDL.h>
#include <iostream>

int main(int argc, char* argv[]) {
    SDL_Init(SDL_INIT_VIDEO);

    SDL_Window* window = SDL_CreateWindow("SDL Event Demo", SDL_WINDOWPOS_UNDEFINED, SDL_WINDOWPOS_UNDEFINED, 640, 480, 0);
    if (window == NULL) {
        std::cout << "Could not create window: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_Event event;
    bool running = true;
    while (running) {
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT) {
                running = false;
            }
            if (event.type == SDL_KEYDOWN) {
                std::cout << "Key pressed: " << SDL_GetKeyName(event.key.keysym.sym) << std::endl;
                running = false;
            }
        }
    }

    SDL_DestroyWindow(window);
    SDL_Quit();

    return 0;
}
```

# 4. SDL 线程

# 4.1. SDL 线程函数

1. SDL线程创建：SDL_CreateThread
2. SDL线程等待：SDL_WaitThead
3. SDL互斥锁：SDL_CreateMutex/SDL_DestroyMutex
4. SDL锁定互斥：SDL_LockMutex/SDL_UnlockMutex
5. SDL条件变量(信号量)：SDL_CreateCond/SDL_DestoryCond
6. SDL条件变量(信号量)等待/通知：SDL_CondWait/SDL_CondSingal

# 4.2. code

创建一个线程，每隔 1 秒输出一行日志

```rust
#include <SDL.h>
#include <iostream>

// 线程函数
int threadFunction(void* data) {
    for (int i = 0; i < 10; ++i) {
        SDL_Delay(1000);  // 延迟一秒
        std::cout << "Thread log: " << i << std::endl;
    }
    return 0;
}

int main(int argc, char* argv[]) {
    SDL_Init(SDL_INIT_VIDEO);

    SDL_Thread* thread = SDL_CreateThread(threadFunction, "TestThread", (void*)NULL);
    if (thread == NULL) {
        std::cout << "Could not create thread: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_WaitThread(thread, NULL);

    SDL_Quit();

    return 0;
}
```

# 5. SDL YUV视频显示

# 5.1. 显示流程

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717940887444-66d97455-6ac0-4096-8bd7-74a001f63870.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717940887444-66d97455-6ac0-4096-8bd7-74a001f63870.png)

# 6. SDL 播放PCM音频数据

# 6.1. 打开音频设备

```rust
int SDLCALL SDL_OpenAudio(SDL_AudioSpec * desired, SDL_AudioSpec * obtained);
// desired：期望的参数。
// obtained：实际音频设备的参数，一般情况下设置为NULL即可。
```

**SDL_AudioSpec 结构体 参数详解**

SDL_AudioSpec

typedef struct SDL_AudioSpec {

int freq; // 音频采样率

SDL_AudioFormat format; // 音频数据格式

Uint8 channels; // 声道数: 1 单声道, 2 立体声

Uint8 silence; // 设置静音的值，因为声音采样是有符号的，所以0当然就是这个值

Uint16 samples; // 音频缓冲区中的采样个数，要求必须是2的n次

Uint16 padding; // 考虑到兼容性的一个参数

Uint32 size; // 音频缓冲区的大小，以字节为单位

SDL_AudioCallback callback; // 填充音频缓冲区的回调函数

void *userdata; // 用户自定义的数据

} SDL_AudioSpec

# 6.2. 播放音频

SDL_AudioCallback()函数

```rust
// userdata：SDL_AudioSpec结构中的用户自定义数据，一般情况下可以不用。
// stream：该指针指向需要填充的音频缓冲区。
// len：音频缓冲区的大小（以字节为单位）1024*2*2。
void (SDLCALL * SDL_AudioCallback) (void *userdata, Uint8 *stream, int len);
```

播放音频数据

```rust
// 当pause_on设置为0的时候即可开始播放音频数据。设置为1的时候，将会播放静音的值。
void SDLCALL SDL_PauseAudio(int pause_on)
```

# 6.3. code

```rust
// 文件下载地址
// wget http://streams.videolan.org/samples/MPEG-4/video.mp4
// 转换为yuv420p
// ffmpeg -i video.mp4 -pix_fmt yuv420p -s 640x480 video.yuv

// SDL 播放 YUV 视频 demo
// 从文件中读取 YUV 视频帧，显示到窗口中。
#include <SDL.h>
#include <iostream>
#include <fstream>

const int SCREEN_WIDTH = 640;
const int SCREEN_HEIGHT = 480;

int main(int argc, char* argv[]) {
    SDL_Init(SDL_INIT_VIDEO);

    SDL_Window* window = SDL_CreateWindow("SDL YUV Video Demo", SDL_WINDOWPOS_UNDEFINED, SDL_WINDOWPOS_UNDEFINED, SCREEN_WIDTH, SCREEN_HEIGHT, 0);
    if (window == NULL) {
        std::cout << "Could not create window: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_Renderer* renderer = SDL_CreateRenderer(window, -1, 0);
    if (renderer == NULL) {
        std::cout << "Could not create renderer: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_Texture* texture = SDL_CreateTexture(renderer, SDL_PIXELFORMAT_YV12, SDL_TEXTUREACCESS_STREAMING, SCREEN_WIDTH, SCREEN_HEIGHT);
    if (texture == NULL) {
        std::cout << "Could not create texture: " << SDL_GetError() << std::endl;
        return 1;
    }

    std::ifstream file("video.yuv", std::ios::binary);
    if (!file) {
        std::cout << "Could not open video file" << std::endl;
        return 1;
    }

    char* buffer = new char[SCREEN_WIDTH * SCREEN_HEIGHT * 3 / 2];  // YUV420

    SDL_Event event;
    bool running = true;
    while (running) {
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT) {
                running = false;
            }
        }

        if (!file.read(buffer, SCREEN_WIDTH * SCREEN_HEIGHT * 3 / 2)) {
            std::cout << "End of video file" << std::endl;
            break;
        }

        SDL_UpdateTexture(texture, NULL, buffer, SCREEN_WIDTH);
        SDL_RenderClear(renderer);
        SDL_RenderCopy(renderer, texture, NULL, NULL);
        SDL_RenderPresent(renderer);
    }

    delete[] buffer;
    SDL_DestroyTexture(texture);
    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();

    return 0;
}
```

播放PCM文件的demo

```rust

// SDL 播放 PCM 音频 demo
// 从文件中读取 PCM 音频数据，播放出来。
// ffmpeg -i video.mp4 -f s16le -acodec pcm_s16le audio.pcm
#include <SDL2/SDL.h>
#include <iostream>
#include <fstream>

#define AUDIO_FILE "audio.pcm"
#define AUDIO_FREQ 44100
#define AUDIO_CHANNELS 2
#define AUDIO_SAMPLES 2048
#define AUDIO_FORMAT AUDIO_S16SYS

void audio_callback(void *userdata, Uint8 *stream, int len) {
    std::ifstream *audio_file = reinterpret_cast<std::ifstream*>(userdata);
    audio_file->read(reinterpret_cast<char*>(stream), len);
}

int main(int argc, char* argv[]) {
    if (SDL_Init(SDL_INIT_AUDIO) < 0) {
        std::cerr << "Could not initialize SDL: " << SDL_GetError() << std::endl;
        return 1;
    }

    std::ifstream audio_file(AUDIO_FILE, std::ios::binary);
    if (!audio_file) {
        std::cerr << "Could not open audio file: " << AUDIO_FILE << std::endl;
        return 1;
    }

    SDL_AudioSpec audio_spec;
    audio_spec.freq = AUDIO_FREQ;
    audio_spec.format = AUDIO_FORMAT;
    audio_spec.channels = AUDIO_CHANNELS;
    audio_spec.samples = AUDIO_SAMPLES;
    audio_spec.callback = audio_callback;
    audio_spec.userdata = &audio_file;

    if (SDL_OpenAudio(&audio_spec, NULL) < 0) {
        std::cerr << "Could not open audio: " << SDL_GetError() << std::endl;
        return 1;
    }

    SDL_PauseAudio(0);

    while (audio_file.good()) {
        SDL_Delay(100);
    }

    SDL_CloseAudio();
    SDL_Quit();

    return 0;
}
```