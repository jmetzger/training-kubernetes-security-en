# Kernel Hardening 

## Checker 

```
https://github.com/a13xp0p0v/kernel-hardening-checker?tab=readme-ov-file

# Installation
cd /usr/src
git clone https://github.com/a13xp0p0v/kernel-hardening-checker?tab=readme-ov-file
cd kernel-hardening-checker
```

```
sudo sysctl -a > sysctl.file && ./bin/kernel-hardening-checker -c /boot/config-6.8.0-44-generic -l /proc/cmdline -s sysctl.file
```


## Kernel Defence Map 

  * https://github.com/a13xp0p0v/linux-kernel-defence-map

## Guidelines 

  * https://gist.github.com/dante-robinson/3a2178e43009c8267ac02387633ff8ca
