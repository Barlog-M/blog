+++
title = "Hardware. Thinkpad T14 AMD"
date = 2020-10-09
+++

My current laptop is [Thinkpad T14 AMD](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-t-series/ThinkPad-T14-AMD-G1/p/22TPT14T4A2)

Everything works fine under [Arch Linux](https://www.archlinux.org/).

There is an article from Arch Wiki about almost same model [T14s](<https://wiki.archlinux.org/index.php/Lenovo_Thinkpad_T14s_(AMD)_Gen_1>)

It better to use [libinput](https://wiki.archlinux.org/index.php/Libinput) for touchpad. There is a config file `/etc/X11/xorg.conf.d/70-touchpad.conf`

```conf
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
        Option "AccelSpeed" "0.4"
        Option "Tapping" "on"
        Option "ClickMethod" "clickfinger"
        Option "NaturalScrolling" "false"
        Option "ScrollMethod" "twofinger"
        Option "DisableWhileTyping" "true"
EndSection
```

[Geekbench 5 on power supply](https://browser.geekbench.com/v5/cpu/4103813)

[Geekbench 5 on battery](https://browser.geekbench.com/v5/cpu/4103989)

Helpful article about [Increasing Battery Life on an Arch Linux Laptop](https://austingwalters.com/increasing-battery-life-on-an-arch-linux-laptop-thinkpad-t14s/)
