# 操作系统课程笔记与练习（进程、线程、互斥与信号量）

> 跟着 B 站操作系统课程做的 C 语言练习：fork 进程、pthread 线程、互斥锁、信号量，以及几个经典同步问题。

This is my notebook for OS

OSCLASS url：https://www.bilibili.com/video/BV1bf4y147PZ/?spm_id_from=333.337.search-card.all.click

## 问题

掌握操作系统里的并发基础：进程创建与孤儿进程、线程创建与回收、多线程下对共享数据的竞争，以及用互斥锁和信号量解决同步问题。

## 方案

按课程讲次分目录，每个目录是一个或几个可独立编译运行的 C 程序：

- `L03.process/`：用 `fork` 创建子进程，观察父子进程的 pid 和孤儿进程
- `L05.thread/`：pthread 创建线程；用多线程做蒙特卡洛估算圆周率，对比单线程与多线程版本
- `L07.Mutex/`：用互斥锁保护共享变量，两个售票线程卖最后的票
- `L08.Semaphore/`：用信号量实现同一个售票互斥
- `classic_semaphore_problems/`：生产者消费者、读者写者、理发师、哲学家就餐四个经典问题，哲学家就餐里用注释标出了“会产生死锁”的写法
- `check_test/`：用 `check` 单元测试库写的一个最小测试例子

这些程序是跟着课程自己敲出的练习，代码均为本人所写。除上面各目录外，还包括：`L05.thread/` 里的 `hellothread.c`、`multithreads.c`（线程创建，以及两个线程无保护地递增同一全局变量），`L08.Semaphore/semaphore2.c`（初值为 2 的信号量限制同时通过岔路口的车数）。

## 结果

没有量化的测试结果。每个程序是可运行的练习，行为靠运行时的输出观察；`check_test/` 里只有一个 `add(2,3) == 5` 的断言。

## 复现

需要 Linux（用到 `fork`、`pthread`、POSIX 无名信号量 `sem_init`，macOS 不支持无名信号量）。以互斥锁练习为例：

```bash
gcc -pthread L07.Mutex/mutex_test.c -o mutex_test && ./mutex_test
```

其余程序同理，用到信号量的同样加 `-pthread`；仓库里已有的同名无后缀文件是已编译好的可执行文件。`check_test/` 需要先安装 `check` 库，用 `gcc check_test/testcode.c check_test/test.c $(pkg-config --cflags --libs check)` 编译。

## 证据清单

本项目的证据化清单见 [.portfolio/project.yaml](.portfolio/project.yaml)：每一条贡献和发现都指向仓库里已提交的代码原文。校验命令：`profile-atlas check .`
