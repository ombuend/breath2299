<br>

<img src="https://github.com/MilkyDeveloper/cb-linux/blob/main/docs/assets/banner.png?raw=true" alt="Breath Banner"></img>

# 🙼 ＢＲＥＡＴＨ 

<p align="center">An experimental way to natively run <kbd><img width="25" height="30" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Tux.svg/1200px-Tux.svg.png"></img></kbd> Linux on modern Chromebooks without replacing firmware</p>

## Supported Devices

**All Chromebooks released after 2018 are supported.**

However, this project is being developed on `Nami`, so the following models will have for-sure audio support:
* Acer Chromebook 13 / Spin 13
* Dell Inspiron 14 2-in-1 Model 7486 
* Yoga Chromebook C630
* HP Chromebook x360 14 (i3 8130u)
* Acer Chromebook 715
* Acer Chromebook 714
* HP Chromebook 15 G1
* Dell Inspiron Chromebook 14 (7460)

### Benefits

**Stock Ubuntu:**
* Requires a change in firmware (UEFI or Legacy Boot)
* Has everything working except touchscreen and audio

**Breath:**
* Requires no change in firmware and has all peripherals working on my HP Chromebook 14 x360.

## Running Breath

Due to licensing restraints, you cannot just download an ISO of Breath and flash it. Instead, you *build* the bootable USB.
> Currently, this project can only work on Debian or Ubuntu. Running this on Arch or Fedora is unsupported.

**Prerequisite:** Git is installed and you have a mainstream, fast USB plugged in

1. `git clone https://github.com/MilkyDeveloper/cb-linux && cd cb-linux`
2. `bash setup.sh cli`
(should take ~15 minutes on a 4-core mobile processor)

> * Using the CLI argument installs a minimal CLI environment on the USB. If you would like to install a desktop, you can use `gnome`, `kde`, `minimal`, `deepin`, `xfce`, `lxqt`, `mate` or `openbox` instead of `cli`. You can use `cli` and install a desktop later on the Chromebook with `tasksel`.
> * You can run `bash setup.sh cli arch` to put Arch Linux on the USB. Currently, desktops have to be manually installed on Arch.

3. Done! Now just boot into ChromeOS, enter the shell (<kbd>CTRL</kbd> <kbd>ALT</kbd> <kbd>T</kbd>, `shell`), and run:  
`sudo crossystem dev_boot_usb=1; sudo crossystem dev_boot_signed_only=0; sync`  
to enable USB and Custom Kernel Booting.

Reboot, and with the USB plugged in, press <kbd>CTRL</kbd> <kbd>U</kbd> instead of <kbd>CTRL</kbd> <kbd>D</kbd>. After a short black screen, the system should display a login screen.

### Audio

If your device is one of the devices on the above list, you can enable audio.

Run `setup-audio` once booted into Breath. Reboot and enjoy working audio.

If it is not, please open a Github issue and provide your Chromebook's board name (on the bottom of the developer mode screen).

## How does everything work?

This project uses the ChromeOS Kernel and the firmware. Touchscreen and all other peripherals *just work*. Breath has been carefully designed not to have any legal issues, so you can't flash the ISO or have the audio firmware bundled.

Audio works [perfectly](bin/setup-audio) through ALSA, but not PulseAudio or Pipewire. All apps that use PulseAudio libraries (like Firefox) work as of [this commit](https://github.com/MilkyDeveloper/cb-linux/commit/884bd03b8eef554bdbafd7b4d62f36690f472237). You can follow further audio progress [here](https://github.com/MilkyDeveloper/cb-linux/projects/1).
