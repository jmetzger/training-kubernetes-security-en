# Capabilities 

## What are these ? 

  * Capabilities allow us to execute stuff, that normally only the root user can do.

## Best practice for security and container/pods 

  * Tear capabilities down to Drop: all and set up those, that you need

## As little capabilities are possible. 

  * Use as little capabilities as possible in your pod/cont


## List of capabilities 

 * cap_chown
 * cap_dac_override
 * cap_fowner
 * cap_fsetid
 * cap_kill
 * cap_setgid
 * cap_setuid
 * cap_setpcap
 * cap_net_bind_service
 * cap_net_raw
 * cap_sys_chroot
 * cap_mknod
 * cap_audit_write
 * cap_setfcap

### cap_chown 

  * User can chown (Change Owner without being root)

### cap_dac_override 

  * Bypasses permission checks 

### cap_fowner 

```
Bypass permission checks on operations that normally
require the filesystem UID of the process to match the
UID of the file (e.g., chmod(2), utime(2)),
```

### cap_fsetid 

  * Safe to disable
  * Not needed as we should not use setgid and setuid bits anyway

```
when creating a new folder in folder with setgit, new folder
will have this permission as well
```

### cap_kill 

  * Please not have this enabled.
  * User is allowed to kill processes within the container

```
Bypass permission checks for sending signals
# should not be the job of the container
```

### cap_setgid 

  * Do not enable !

```
Allow to change GID of a process 
```

### cap_setuid 

  * makes it possible to privilege escalations 

```
make arbitrary manipulations of process UID
(setuid(2), setreuid(2), setresuid(2), setfsuid(2));
```

### cap_setpcap 

```
Allow user to set other process capabilities
```

### cap_net_bind_service

  * If you want to bind a privilege port, you will need this
  * Like starting httpd on port 80

```
Security Question/Hint:
Is there probably a better way to do this:
e.g. Open Port 8080 -> and having the service on port 80
```

### cap_net_raw

  * Needed to open a raw socket
  * Needed to perform ping 
  * There have been many vulnerabilites concerning this capability in the past e.g. [CVE-2020-14385](https://www.alibabacloud.com/help/en/ack/product-overview/vulnerability-updates-cve-2020-14386)
  * Warning: Do not activate it, if you really, really need this
    * You can ping with a debug container if you need to
   
### cap_sys_chroot

```
CAP_SYS_CHROOT permits the use of the chroot(2) system call. This may allow escaping of any chroot(2) environment, using known weaknesses and 
```

### cap_mknod
 
  * No need to have this 
  * Allow to create special files under /dev 

### cap_audit_write

  * Allow to write to kernel audit log 

### cap_setfcap

  * Allow user to set other file capabilities

## Documentation 

  * https://man7.org/linux/man-pages/man7/capabilities.7.html
