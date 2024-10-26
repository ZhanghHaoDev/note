# 第一章 关于UNIX系统开发的学习

## 1. UNIX开发简介

## 2. UNIX系统开发的知识体系

1. C语言的学习
3. UNIX系统编程的学习
4. UNIX网络编程的学习
5. CMake的学习
6. Makefile的学习

## 3. 关于POSIX标准的学习

1. 什么是POSIX标准

POSIX标准是Portable Operating System Interface of UNIX的缩写，是IEEE制定的一种标准，用于定义操作系统的接口。POSIX标准的目的是为了使UNIX系统的程序能够在其他操作系统上编译和运行。

POSIX标准本质上是一套接口规则，用于定义操作系统的接口，使得应用程序可以在不同的UNIX系统上编译和运行。POSIX标准旨在提高应用程序的可移植性，使得它们可以在不同的操作系统（如Linux的不同发行版、macOS、FreeBSD等）上运行，而无需进行大量的修改。

2. POSIX标准的内容

POSIX标准涵盖了多个方面，包括基本系统接口、线程、I/O、时间和日期、用户和组等。以下是POSIX标准的主要内容：

1. 基本系统接口
POSIX标准定义了一组基本的系统接口，用于文件操作、进程控制、信号处理等。
+ 文件操作：
    open、close、read、write、lseek、stat、fstat、lstat等。
+ 进程控制：
    fork、exec、wait、waitpid、getpid、getppid等。
+ 信号处理：
    signal、sigaction、raise、kill、sigprocmask等。

2. 线程
POSIX标准定义了一组线程接口，用于线程的创建、同步、互斥等。
+ 线程创建和管理：
    pthread_create、pthread_join、pthread_exit、pthread_self等。
+ 线程同步：
    pthread_mutex_init、pthread_mutex_lock、pthread_mutex_unlock、pthread_cond_wait、pthread_cond_signal等

3. I/O
POSIX标准定义了一组I/O接口，用于文件I/O、网络I/O等。
+ 文件I/O：
    open、close、read、write、lseek等。
+ 网络I/O：
    socket、bind、listen、accept、connect、send、recv等。

4. 时间和日期
POSIX标准定义了一组时间和日期接口，用于时间获取、定时器等。
+ 时间获取：
    time、gettimeofday、clock_gettime等。
+ 定时器：
    alarm、sleep、nanosleep等。

5. 用户和组
POSIX标准定义了一组用户和组接口，用于用户ID、组ID的管理等。
+ 用户ID和组ID：
    getuid、geteuid、getgid、getegid、setuid、setgid等。