
# NuttX RISC-V

## Pre-requirement

    Install RISC-V toolchains

    $ git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
    $ cd riscv-gnu-toolchain/
    $ mkdir build && cd build
    $ ../configure --prefix=/opt/riscv --enable-multilib
    $ sudo make
    $ export PATH=$PATH:/opt/riscv/bin

## Install qemu

    $ export CURDIR=`pwd`
    $ git clone https://github.com/qemu/qemu
    $ cd ${CURDIR}/qemu/
    $ ./configure --target-list=riscv32-softmmu
    $ make
    $ sudo make install

## Get Nuttx

    $ cd ${CURDIR}
    $ git clone https://github.com/apache/incubator-nuttx.git nuttx
    $ git clone https://github.com/apache/incubator-nuttx-apps.git apps
    $ git clone https://starcat-io@bitbucket.org/nuttx/tools.git tools

## Install kconfig-frontends

    $ cd ${CURDIR}/tools/kconfig-frontends
    $ ./configure --enable-mconf --disable-nconf --disable-gconf --disable-qconf
    $ make
    $ sudo make install

## Build applications

    $ cd ${CURDIR}/nuttx/
    $ ./tools/configure.sh hifive1-revb:nsh
    $ make menuconfig
    $ make

## Run qemu

    $ cd ${CURDIR}/nuttx
    $ qemu-system-riscv32 -nographic -machine sifive_e -kernel ./nuttx

