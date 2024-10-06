---
title : 'Nuttx dengan Qemu'
date : 2024-10-06T14:21:53+07:00
summary : "Bagian ini adalah catatan tentang menjalankan nuttx dengan Qemu"
description : "Bagian ini adalah catatan tentang menjalankan nuttx dengan Qemu"
toc: true
readTime: true
autonumber: true
math: true
tags: ["NuttX", "C", "Embedded"]
showTags: false
hideBackToTop: false
---

Qemu merupakan sebuah emulator yang bagus untuk mensimulasikan linux lalu bagaimana jika kita ingin menggunakan NuttX yang dijalanakan melalui Qemu. Oh tentu saja bisa kita bisa membuild code nuttx dan melakukannya berjalan pada emulator Qemu. Seperti halnya membuat program aplikasi dengan menggunakan linux, maksudnya membuild sebuah sistem operating linux kita perlu mendownload code source tools dan apps untuk nuttx. Pertama buat direktori untuk pengerjaan NuttX dengan qemu. 

```bash
mkdir ~/NuttXqemu
cd ~/NuttXqemu
```

Kemudian mendownload code NuttX untuk kita build nanti

```bash
git clone https://github.com/apache/incubator-nuttx.git nuttx
git clone https://github.com/apache/incubator-nuttx-apps apps
```

sebelumnya kita perlu menginstall gcc untuk arm untuk melakukan compile dan linker. 
```bash
sudo apt install gcc-arm-none-eabi.
```
lalu kita build dengan code berikut
```bash
./tools/configure.sh -l qemu-armv7a:nsh
make
```

lalu run dengan code berikut
```bash
qemu-system-arm -cpu cortex-a7 -nographic \
     -machine virt,virtualization=off,gic-version=2 \
     -net none -chardev stdio,id=con,mux=on -serial chardev:con \
     -mon chardev=con,mode=readline -kernel ./nuttx
```
nanti akan muncul code qemu dengan nuttx yang ada didalamnya. Qemu akan mensimulasikan hardware armv7a 

# Referensi 
1. [Build dengan Qemu](https://nuttx.apache.org/docs/latest/platforms/arm/qemu/boards/qemu-armv7a/index.html)







