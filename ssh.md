# ssh

## ssh tunnel实现反向代理

假设在内网有一个自己的电脑IN，希望在外网访问内网资源。由于内网电脑没有公网IP，所以外网无法直接向内网电脑发起连接。为实现我们的目标，需要从内网电脑主动向一个外网服务器（具有公网IP即可）发起一个连接，外网通过这个服务器使用这一连接，再通过内网电脑访问内网资源。

外网 -> 服务器（S） <-> 内网主机（I） -> 内网

在内网电脑上操作，将外网服务器的localhost地址和内网主机映射起来，外网服务器localhost的222端口映射到内网主机的22端口。同时，外网服务器SERVER_IP的PORT端口映射到localhost的222端口。222和22可以替换为其他端口号。

SERVER_IP:PORT <-> localhost:222 <-> 内网主机:22

```bash
# Add -v to the ssh command to get some debugging information
$ ssh -CR 222:localhost:22 SERVER_USER@SERVER_IP
# 输入root密码登陆外网服务器
# -4 use ipv4，server_ip=0.0.0.0/192.168.0.1/localhost
ssh -CfND SERVER_IP:PORT -p 222 LOCAL_USER@localhost
# 输入LOCAL_USER密码完成与内网主机的连接
# 测试
curl --socks5 SERVER_IP:PORT LOCAL_SITE
```

其中：

- `SERVER_USER`为外网服务器的用户名
- `SERVER_IP`为外网服务器的公网IP或域名
- `LOCAL_USER`为内网主机的用户名
- `LOCAL_SITE`为内网站点

参考资料
- [Proxy Using SSH Tunnel](http://www.systutorials.com/944/proxy-using-ssh-tunnel/)
- [SSH Port Forwarding on Linux](http://www.systutorials.com/39648/port-forwarding-using-ssh-tunnel/)
- [What does the Broken pipe message mean in an SSH session?](http://unix.stackexchange.com/questions/2010/what-does-the-broken-pipe-message-mean-in-an-ssh-session)
- [怎样从外网访问内网服务器](http://www.cnblogs.com/devymex/p/4156378.html)
- [ssh tunnel - bind: Cannot assign requested address](http://serverfault.com/questions/444295/ssh-tunnel-bind-cannot-assign-requested-address)

如果配置未成功，检查sshd的配置，确保ssh配置如下
```
vi /etc/ssh/sshd_config
GatewayPorts yes
PermitTunnel yes
TCPKeepAlive yes
AllowTCPForwarding yes
PermitOpen any
```