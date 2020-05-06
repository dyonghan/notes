# python ip

优先使用python3(2.7部分新版本)自带的`ipaddress`库。

```python
def is_ip_in_net(ip, net):
    netaddr, masknum = net.split('/')
    ipbits = socket.inet_aton(ip)
    netbits = socket.inet_aton(net)
    iplint=struct.unpack('!I', ipbits)[0]
    netlint=struct.unpack('!I', netbits)[0]
    host_bit = 32 - int(masknum)
    masklint = (0xFFFFFFFF<<host_bit) & 0xFFFFFFFF

    return (iplint & masklint) == (netlint & masklint)

def mask_addr2num(maskaddr):
    masknum = sum([bin(int(x)).count('1') for x in maskaddr.split('.')])
    return str(masknum)
```
