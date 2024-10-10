# Harden os and Kernel 

## Kernel 

  * Always patch to the newest kernel
  * Be sure to restart the server (in most cases new kernel will start to get used after reboot)

### Good tool for detecting great hardening kernel parameter 

  * Kernel hardening checker

### Modules 

```
# sysctl -w kernel.modules_disabled=1
kernel.modules_disabled = 1
```
    * If possible harden your kernel, e.g.
    * But of course, it is then not allowed to load modules after that isset 

## OS 

  * Only install the really needed software in os
    * Eventuall start from a minimal image 
  * Close unneeded ports 

## OS-Patching 

  * Patch frequently. Eventually using

## Hardening Guide

  * A bit older, but has really good hints

[Telekom Hardening Guide](https://github.com/jmetzger/TelekomSecurity.Compliance.Framework)
