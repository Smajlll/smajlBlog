---
title: Jak úspěšně (ne)spustit QUEMU ve WSL
date: 2023-10-12 21:20:49
tags:
- qemu
- linux
- wsl
- windows
- programming
---

## Jak úspěšně (ne)spustit QUEMU ve WSL

Ahoj Ahoj, tady zase a znova Vítek. Dneska jsem si za úkol dal jednoduše, spustit pomocí QEMU VM Počitač ve WSL
Takže, začneme jednoduše, zapnul jsem si powershell a spustil jsem příkaz:

``` bash
$ wsl --update && wsl --install -d Debian
```

Dál jsem nastalvil username a heslo a byl jsem v BASHi.
Ale před tím než nainstalujeme QEMU si aktualizujeme systém, takže:

``` bash
$ sudo apt update -y && sudo apt upgrade -y
```

Potom už stačilo jenom nainstalovat QEMU a dalši potřebné věcičky

``` bash
$ sudo apt install wget unzip quemu
```

No a co teď? No teď už můžeme začít využívat QEMU pomocí X11
Před začátkem jsem si vytvořil složku

``` bash
$ mkdir cos && cd cos
```

A stáhl jsem si soubor s .img souborem a rozbalil jsem ho

``` bash
$ unzip chromeos_15117.112.0_reven_recovery_stable-channel_mp-v2.bin.zip
```

A vytvořil jsem si virtuální HDD pro QEMU s velikostí 20GB

``` bash
$ qemu-img create disk.img 20G
```

a pokusil jsem se nabootovat pomocí příkazu:

``` bash
$ sudo qemu-system-x86_64 -enable-kvm -m 6G -smp 4 -machine q35 -cpu host -device virtio-vga-gl -rtc base=utc -hda chromeos_15117.112.0_reven_recovery_stable-channel_mp-v2.bin -hdb disk.img -display gtk,gl=on,show-cursor=on -usb -device usb-tablet
```

A ono nic? - Ano přesně tak, skončil jsem s chybou:

``` bash
Couldnt open libEGL.so.1: libEGL.so.1: cannot open shared object file: No such file or directory; Aborted
```

A bohužel jsem se dál zatím nedostal, budu poskytovat updaty s mým pokrokem. Tady byl Vítek, a zatím ✌️
