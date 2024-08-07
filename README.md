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

