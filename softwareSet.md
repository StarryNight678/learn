#Windows


1. Windows 10 下我一直抱怨它对于内存占用不够积极，原来是 Windows File Cache 默认设定的问题，改为 Level 2 后，File Cache 就积极了很多，
cmd 管理员模式运行

```

fsutil behavior set memoryusage 2

```


#  VMware
1.  bridged(桥接模式)
当采用桥接时，VMWare会虚拟一块网卡（VMnet0）和真正的物理网卡就行连接.要么都能联网,要么都不能.
那么，发到物理网卡的所有数据包就到了VMWare虚拟机，而由VMWare发出的数据包也会通过桥从物理网卡的那端发出 
在桥接时，VMWare网卡和物理网卡应该处于同一ip网段，所以在虚拟机中ping物理网卡ip，或者在主机总ping虚拟机网卡ip，都可以ping通
2. NAT(网络地址转换模式)
NAT是为了让私有IP段能够访问Internet而开发
VMWare的NAT上网采用的技术是在主机和虚拟机之间用软件伪造出一块网卡（VMnet8），这块网卡和虚拟机的ip处于同一网段
同时，在这块网卡和主机的网络接口之间进行NAT、虚拟机发出的每一个数据包都会经过虚拟网卡，然后NAT，然后由主机的接口发出
由于在这种条件下，虚拟机和主机不在同一个ip段，但是主机相当于虚拟机的网关，所以虚拟机能ping通主机，而主机ping不通虚拟机
3. Host(主机模式)
顾名思义，这种技术提供的是主机和虚拟机之间的网络互访，而不是虚拟机访问internet的技术
如果，
只想让虚拟机和主机之间有数据交换，而不想让虚拟机访问internet，就要采用这个设置  
