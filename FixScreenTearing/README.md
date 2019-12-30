
# Screen tearing fix

## Used platform
```
Distributor ID: Ubuntu
Description:    Ubuntu 19.10
Release:        19.10
Codename:       eoan
Kernel version: 5.3.0-24-generic
```

## Issue
When connecting external displays I experienced a tremendous drop in framerate and screen tearing. By using various web sources and some experimenting, I managed to put together a working solution.

## Solution
1. Install the `xserver-xorg-video-intel` package:
    ```bash
    sudo apt install xserver-xorg-video-intel
    ```
2. Place the `20-intel.conf` file in `/usr/share/X11/xorg.conf.d/` directory and reboot the system.
3. If this worked, ***awesome!*** <br> Otherwise, continue.
4. Check that your actual GPU PCI bus id matches the one in your `20-intel.conf` file (Line with `BusID`):
    ```bash
    $ lspci -k | grep -iEA5 'vga|3d|display'
    00:02.0 VGA compatible controller: Intel Corporation Skylake GT2 [HD Graphics 520] (rev 07)
            Subsystem: Lenovo Skylake GT2 [HD Graphics 520]
            Kernel driver in use: i915
            Kernel modules: i915
    ```
    "`00:02.0`" means that the BusID value should be set to "`PCI:0:2:0`".
## Sources
- [Xorg Screen Tearing Issue on Intel Integrated Graphics](https://www.linuxquestions.org/questions/linux-newbie-8/xorg-screen-tearing-issue-on-intel-integrated-graphics-4175647941/)
- [intel gfx, screen tearing solved!](https://www.linux.org/threads/intel-gfx-screen-tearing-solved.20489/)
- [How to get the GPU info?](https://askubuntu.com/questions/5417/how-to-get-the-gpu-info)
- [Linux Find Out Graphics Card Installed In My System](https://www.cyberciti.biz/faq/linux-tell-which-graphics-vga-card-installed/)


