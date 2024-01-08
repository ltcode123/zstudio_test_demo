# 注意：本文件为公司内部构建测试参考文件，描述过于口语化不宜直接用于商用指导实例，发行前应当将本文件删除。

# 参考链接：https://blog.csdn.net/qq_42357476/article/details/127315647
# 必看 详细的构建仿真流程请参考：https://terapines.feishu.cn/docx/O2Lkd30igokIPaxMMt9cEeCYnkg

# 构建流程
1、(如果已经安装了完整的工具链此步骤可以省略)下载相关依赖：sudo apt-get install ninja-build libglib2.0-dev libpixman-1-dev
2、(如果已经安装了完整的工具链此步骤可以省略)由于这里没有32位的qemu，所以我自己下载编译了一个，流程如下：
    wget https://download.qemu.org/qemu-7.1.0.tar.xz
    tar xvJf qemu-7.1.0.tar.xz
    cd qemu-7.1.0
    ./configure
    make
    sudo make install

3、命令行进入You path/FreeRTOS/Demo/RISC-V-Qemu-virt_GCC目录


4、修改位于RISC-V-Qemu-virt_GCC目录下的Makefile，在makefile中的CROSS变量指定自己的工具链路径，如：
    CROSS   = /home/lt/work/SDK/hpmicro/riscv32-unknown-elf-newlib-multilib/bin/riscv32-unknown-elf-


5、在RISC-V-Qemu-virt_GCC目录下执行make命令编译freeRTOS，编译好的qemu仿真文件位于build目录下

6、执行/usr/local/bin/qemu-system-riscv32 -nographic -machine virt -net none -chardev stdio,id=con,mux=on -serial chardev:con -mon chardev=con,mode=readline -bios none -smp 4 -kernel build/RTOSDemo.axf命令，在qemu上运行FreeRTOS

## 注：在Makefile中建议使用riscv32-unknown-elf-的工具链和qemu-system-riscv32仿真器


7、确认自己的QemuVirt.json位置
zemu运行：/home/lt/APP/Terapines/zcc20240104/build-zcc/zemu/src/simulate/Driver/zemu --board /home/lt/APP/Terapines/zcc20240104/install-zcc/config/zvb/demos/virtual-boards/QemuVirt.json --fs --bios ./build/RTOSDemo.axf


# 如有疑问请邮件联系：tao.liang@terapines.com

