# proj2-os-kernels-by-history

### 项目描述
当前大学本科学生做OS实验面临工作量大，实验指导针对性不够强，难以对OS有整体理解等困难。为此，我们希望重新设计面向一般学生，能帮助他们
理解OS课程中各种概念的简洁明了的OS Kernels。同学们将发现，几百行高级语言为主编写的OS Kernel就能体现操作系统中各种抽象的概念。
设计实现这些简洁明了的OS Kernels的目的是：“给学生逐步设计实现OS的线索和参考实例，提高学生的OS分析能力和动手能力，强化学生对 OS 的整体观念”。
这一系列OS kernels的特点是：以CS发展的历史过程为导向，以满足应用需求为基准，实现相对独立，功能简单明确。

为此，我们采用了如下的规划思路：
- 在硬件方面，我们选择了便于OS设计实现的RISC-V硬件平台（基于虚拟硬件模拟器QEMU和物理硬件Kendryte K210（含MMU和S模式）；
- 在软件编程语言方面，我们选择了Rust和C编程语言，当然选择其它语言（Go,Nim,Swift, V-lang...）也是鼓励的。
- 在实验阶段上，大致仿照OS的发展历史来分阶段，每个OS kernel都算是一个历史阶段的OS的缩影，并有多个step组成，解决一两个明确的应用需求。
- 对实现的具体细节不限，只要能通过有明确操作系统服务接口描述的应用测实例即可算完成实验。

### 当前项目相关的实现源码：
- （基于Rust语言）：https://github.com/rcore-os/rCore-Tutorial-v3
- （基于C语言）：https://github.com/DeathWish5/ucore-Tutorial
- 各种实验尝试：https://github.com/chyyuu/os_kernel_lab 中各种包含“v4”的branch，与下面的第0题相关

### 所属赛道

2022全国大学生操作系统比赛的“OS功能设计”赛道

### 参赛要求
- 以小组为单位参赛，最多三人一个小组，且小组成员是来自同一所高校的本科生（2022年春季学期或之后本科毕业的大一~大四的学生）或研究生
- 如学生参加了多个项目，参赛学生选择一个自己参加的项目参与评奖
- 请遵循“2022全国大学生操作系统比赛”的章程和技术方案要求

### 项目导师

任炬 renju@tsinghua.edu.cn 

吴一凡
- github https://github.com/wyfcyx
- email shinbokuow@163.com

### 难度

初等~中等

### 特征

- OS基于RISC-V SBI 规范（大大简化了驱动设计实现）
- 对类 Unix 操作系统有很好的参照
- 可完全使用 Rust 语言或C语言实现
- 支持 QEMU 仿真器（RISC-V）
- 支持 Kendryte K210（含MMU和S模式）

### 文档
- [中文介绍ppt](rCore-Tutorial.pdf)
- [从零开始基于 Rust 写 OS 的学习指导（无需 Rust 和 RISC-V 基础）](https://github.com/rcore-os/rCore/wiki/os-tutorial-summer-of-code)
- [R:Z 从零开始的RustOS编写体验指南](https://simonkorl.gitbook.io/r-z-rustos-guide/)
- [rCore-Tutorial-v3 文档（Rust 语言）](https://rcore-os.github.io/rCore-Tutorial-Book-v3/)
- [Philipp Oppermann写的"Writing an OS in Rust"中文版](https://os.phil-opp.com/zh-CN/)
- [Rust no-std常见问题 en](https://justjjy.com/Rust-no-std)
- [zcore](https://github.com/rcore-os/zCore)
- [uCore-Tutorial 文档（C 语言）](https://github.com/DeathWish5/ucore-Tutorial-Book)
- [uCore-riscv64 文档（C 语言）](https://nankai.gitbook.io/ucore-os-on-risc-v64)

### 平台实现的注意事项

- Rust版本的OS kernels的不少组件 能库（Rust中的crates）的形式重用。
- 目前，在 QEMU 和 K210 平台上支持 CLINT 和 PLIC 外围设备。

### License

- GPL-3 license

## 预期目标

### 注意：下面的内容是建议内容，不要求必须全部完成。选择本项目的同学也可与导师联系，提出自己的新想法，如导师认可，可加入预期目标

在现有OS kernels的基础上，进一步完成如下目标OS kernels（编程语言不限；鼓励用Rust编程）：

### 第0题：支持更方便地开发OS的实验设计

- 设计实现实验节点：体现实验过程或节点的分离性、可组合性和重用性
  - 实验过程中的所有路径集合形成了一个数学上的格状（或具有上下层次关系的网状）结构。格的下界点（网的最低点）是“显示helloworld”的最弱OS；格的上界点（网的最高点）是“显示helloworld”的“具有基本ucore功能”的完整的类UNIX OS；格中不同层次有连线的点具有某种上下依赖关系（即格的偏序,即实现上具有先后关系），没有连线的点不具有某种上下依赖关系（即实现上没有先后关系）。有些点的内核功能是下层的点的组合或改进的组合，可以形成一个crate，并被高层的点合并或组合。
  - 学生完成实验的过程，其实就是通过某条由合理的点集构成的路径（点集构成的线）实现从一个最低点“显示helloworld”的最弱OS逐步到达最高点“具有基本ucore功能”的完整类UNIX OS的。这条线中，从最低点开始的每个线段形成了一个特定功能的OS。
  - 部分具有一定可重用的点形成crate，并被学生以搭积木的形式重用或改造形成新的OS。
- 设计实现OS执行环境：使得实验过程中OS模块具有用户态特性、可调试性
  - 为了让学生实习的OS内核模块（不用修改）的90%以上都能在用户态运行，100%能在内核态运行，需要设计形成OS模块执行所需的用户态执行环境（user execution environment）和内核态执行环境（supervisor execution environment）。这样带了的好处是，学生可以充分利用已经熟悉的IDE环境进行程序开发和调试。并能以比较小的代价完成实验。
  - 在内核态支持gdb命令行方式的debug，这样学生能进行调试。（目前还不知如何做到支持IDE级的调试）
  - 在内核态支持panic的backtrace调用栈显示，这样学生比较清楚问题出在哪里。
  - 改进QEMU或直接修改terminus模拟器，更好地提供程序崩溃的帮助提示或Debug能力。
- 设计实验步骤：
  - 理解分析阶段：通过阅读文档，代码和调试运行代码来理解分析参考OS实验中的各设计步骤中的节点OS。
  - 设计实践阶段：完成实验路线中的各个步骤，学生可以参考或自行设计OS实现路线，在特定阶段，能通过各个独立点的测试用例，最终完成最终节点（类UNIX小OS）的测试用例。每个节点阶段可能形成具有一定完整功能的crate，可用于组合中间/最终节点OS，在功能，性能，可靠性等方面比早期提供的参考OS要性能强，功能多，更可靠。
  - [可选]修复bug阶段：提供相对完整的step by step的一条线，学生可以看到开发的全过程。但线中的某些点（代表进行到的某些阶段）有bug，需要学生分析并fix bug。
  
### 第一题：支持虚存的换入换出功能

- 在QEMU（RV-64）和Kendryte K210开发板上，实现内存到 virtio-blk（qemu）和SD卡（K210开发板）上的换入换出；
- 实现各种页替换算法，并进行初步的性能比较；
- 撰写OS kernel设计与分析文档。

### 第二题：支持多核

- 在QEMU（RV-64）和Kendryte K210开发板上，支持多核，能够进行应用程序的并行处理；
- 实现用户态支持线程机制，有基本的线程管理相关的系统调用（线程创建，线程join，线程退出，线程互斥访问等）
- 实现多种内核同步互斥机制，并在内核中的不同模块应用这些同步互斥机制，实现高效率的并行；
- 撰写OS kernel设计与分析文档。

### 第三题：支持日志文件系统

- 在QEMU（RV-64）和Kendryte K210开发板上，实现一种日志文件系统；
- 能支持异常掉电和系统崩溃后的文件一致性；
- 文件系统有更加全面的文件访问能力（多级目录，硬链接等），支持多核并行方式处理，比单核情况下的性能要高；
- 撰写OS kernel设计与分析文档。

### 第四题：支持网络
- 在QEMU（RV-64）和Kendryte K210开发板上，实现简单的网络驱动（qemu：virtio；k210：有基于spi的wifi，类似串口等）和网络协议栈；
- 能支持基本的socket编程；
- 能运行简单的 Server，可以自己编写，也可以移植自著名开源实现 Nginx 等；
- 撰写OS kernel设计与分析文档。

### 第五题：体现OS各种功能、Bugs和跨硬件能力
- 实现目前没有实现的各种OS功能（如具有图形显示能力，支持树莓派，支持x86等）；
- 在QEMU（RV-64）和Kendryte K210开发板上，设计各种Bugs或更小粒度的steps，来帮助学生更好理解和完成各种OS kernel的实现；
- 实现OS kernel上的简化的lib库，并让更多的教学应用（如教学用的编译器，教学用网络协议栈，教学用算法/数据结构，教学用database等）能运行在这个OS kernel上；
- 撰写OS kernel设计与分析文档。


### 第六题：Rust Std就是OS kernel
在操作系统的发展史上，C语言是为UNIX而生的，也许Rust语言也可以为新一代的OS而生。要达到这一点，我们可以试试能否把Rust的基础库直接放到OS内核中，这样让Rust编译器直接编译出各种
基于Rust Std库的内核模块，为新一代的OS添砖加瓦。

- 让Rust Std绕过系统调用成为OS kernel的核心层；
- 可以在[zcore](https://github.com/rcore-os/zCore)或其他操作系统上进行实现；
- 撰写OS kernel设计与分析文档。

#### 相关参考
- [rusty-hermit](https://github.com/hermitcore/rusty-hermit)
  - [rusty-hermit portal](https://rust-osdev.com/showcase/rusty-hermit/)
  - [paper:RustyHermit: A Scalable, Rust-Based Virtual Execution Environment](https://link.springer.com/chapter/10.1007/978-3-030-59851-8_22)
  - [paper:Exploring Rust for Unikernel Development](https://dl.acm.org/doi/pdf/10.1145/3365137.3365395)
- [Theseus: an Experiment in Operating System Structure and State Management](https://www.usenix.org/system/files/osdi20-boos.pdf) 
  - [Theseus OS project](https://github.com/theseus-os/Theseus),Kevin Boos, Rice University; Namitha Liyanage, Yale University; Ramla Ijaz, Rice University; Lin Zhong, Yale University, - OSDI 2020  
- [The benefits and costs of writing a POSIX kernel in a high-level language](https://pdos.csail.mit.edu/papers/biscuit.pdf),Cody Cutler, M. Frans Kaashoek, and Robert T. Morris,OSDI 2018    
  - the biscuit POSIX-like OS in GO language
  - [biscuit os project](https://pdos.csail.mit.edu/projects/biscuit.html)
- [rust std syscall 简单分析](https://github.com/DeathWish5/SomeBlogs/blob/master/rust%20std%20syscall%20%E5%88%86%E6%9E%90.md)

