# Ubuntu 24.04
## Install .deb package
```bash
sudo dpkg -i package_name.deb
```
## Nvidia X configuration save

```bash
sudo chmod u+x /usr/share/screen-resolution-extra/nvidia-polkit
```

# Fedora

## Install Nvidia Driver with Secure Boot

```bash
sudo dnf install kmodtool akmods mokutil openssl
```

```bash
sudo kmodgenca -a
```

```bash
sudo mokutil --import /etc/pki/akmods/certs/public_key.der
```

```bash
systemctl reboot
```

ENROLL MOK

```bash
sudo dnf install akmod-nvidia
```

```bash
sudo dnf install xorg-x11-drv-nvidia-cuda
```

## Use DSLR as Webcam

```bash
sudo dnf install gphoto2 v4l2loopback ffmpeg
```

```bash
sudo modprobe v4l2loopback exclusive_caps=1 max_buffers=2
```

Loading this kernel module manually (through modprobe) means you will have to remember to modprobe every time you reboot. To ensure this module is enabled when your system is booted, you need to edit one config file /etc/modules, and create a new module config file /etc/modprobe.d/dslr-webcam.conf:

```bash
  $ sudo nano /etc/modules

  # /etc/modules: kernel modules to load at boot time.
  #
  # This file contains the names of kernel modules that should be loaded
  # at boot time, one per line. Lines beginning with "#" are ignored.

  dslr-webcam
```

```bash
  $ sudo nano /etc/modprobe.d/dslr-webcam.conf

  # Module options for Video4Linux, needed for our DSLR Webcam
  alias dslr-webcam v4l2loopback
  options v4l2loopback exclusive_caps=1 max_buffers=2
```

Connect camera stream:

```bash
gphoto2 --stdout --capture-movie | ffmpeg \
-hwaccel nvdec \
-c:v mjpeg_cuvid \
-i - \
-vcodec rawvideo \
-pix_fmt yuv420p \
-threads 0 \
-f v4l2 /dev/video0
```




