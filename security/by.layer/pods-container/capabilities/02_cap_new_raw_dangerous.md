# Why is the capability cap_net_raw dangerous ?

## Recoommendation: Do not add CAP_NET_RAW to the capabilities of your container

   * only reason: you really need ping
   * but you can still use a debug container with ping and the capabilities


## Explanation (Security Wise)

```
CAP_NET_RAW: Any kind of packet can be forged, which includes faking senders, sending malformed packets,
etc., this also allows to bind to any address (associated to the ability to fake a sender this allows to
impersonate a device, legitimately used for "transparent proxying" as per the manpage but from an attacker
point-of-view this term is a synonym for Man-in-The-Middle),
```

## net hijacking

  * old cgroups v1
  * https://0xn3va.gitbook.io/cheat-sheets/container/escaping/excessive-capabilities

  * 
