---
title: Spouštění ChromeOS Flex v QEMU
date: 2022-12-20 21:13:12
tags:
- qemu
- linux
- ChromeOS
- programming
---

## Spouštění ChromeOS Flex v QEMU

Ahoj, tady zas a znova Vítek. Dneska jsem se pokusil a dokonce se mi i povedlo spustit Google ChromeOS Flex v QEMU na svém Arch Linuxu :D
Takže, než začneme, budeme potřebovat nainstalovat QEMU, unzip a wget, dále si taky stáhnout .bin soubor pro ChromeOS Flex.

Na mém počítači je instalace potřebných programů je vcelku jednoduchá. Stačí napsat příkaz

``` bash
$ yay -S wget unzip qemu qemu-kvm
```

Dále jsem si stáhnul nejnovější recovery soubor pro ChromeOS Flex ze stránky Chromium Dash

``` bash
wget https://dl.google.com/dl/edgedl/chromeos/recovery/chromeos_15117.112.0_reven_recovery_stable-channel_mp-v2.bin.zip
```

Tento příkaz stáhnul .zip soubor pro momentální nejnovější verzi ChromeOS Flex, 107.
Dále jsem stažený soubor extrahoval pomocí příkazu unzip

``` bash
$ unzip chromeos_15117.112.0_reven_recovery_stable-channel_mp-v2.bin.zip
```

A už zbývá jen pár posledních kroků. Prvně si musíme vytvořit alespoň 20GB virtuální disk. Já jsem vytvořil disk s velikostí 20GB tímto příkazem:

``` bash
$ qemu-img create disk.img 20G
```

A teď už jsme připraveni nabootovat do ChromeOS Flex Instalace. To uděláme pomocí příkazu:

``` bash
$ qemu-system-x86_64 -enable-kvm -m Kolik Ramky chcete dát ChromeOS Flex -smp 4 -machine q35 -cpu host -device virtio-vga-gl -rtc base=utc -hda Jméno Vašeho Recovery Souboru s příponou .bin -hdb disk.img -display gtk,gl=on,show-cursor=on -usb -device usb-tablet
```

Jako input zařízení používáme Virtuální grafický tablet, protože ChromeOS Flex nemá rádo Virtuální myš QEMU. Tím pádem přijdeme o scrollování a pravé tlačítko. Scrollování můžeme nahradit tažením, jako když chceme přetáhnout ikony. Bohužel jsem žádnou náhradu pro pravé tlačítko myši nenašel.

A máme hotovo, po cvíli by jste měli vidět logo ChromeOS Flex a dále uvítací obrazovku! Nyní již můžete nainstalovat ChromeOS Flex, pomocí stisknutí tlačítka **Next** v pravém dolním rohu, a poté znovu zvolít Next s označenou možností **Install ChromeOS Flex** a po potvrzení instalace, bude systém nainstalován na disk.img který jsme vytvořili před chvílí.

Po instalaci můžete vypnout systém a nabootovat přímo do systému z našeho disk.img na který jsme nainstalovali ChromeOS Flex pomocí příkazu:

``` bash
$ qemu-system-x86_64 -enable-kvm -m Kolik Ramky chcete dát ChromeOS Flex -smp 4 -machine q35 -cpu host -device virtio-vga-gl -rtc base=utc -display gtk,gl=on,show-cursor=on -usb -device usb-tablet -hda disk.img
```

A máme hotovo! Po zadání příkazu nahoře, by mělo ChromeOS Flex nabootovat na stejnou uvítací obrazovku jako při instalaci, ale nyní již bootujeme z disk.img. Můžeme projít prvotní instalací a přihlásit se naším Google účtem a užít si používání ChromeOS Flex.

Díky za přečtení, pokud máte nějaké otázky, pište mi na Discord @smoliicek. Mějte se, smějte se a ✌️