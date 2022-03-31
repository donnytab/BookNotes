第一篇 TCP/IP协议详解

第1章 TCP/IP协议族
1.
    --------------------------------------------------
    应用层        ping, telnet, OSPF, DNS             用户空间
    -------------------------------------- socket ----
    传输层        TCP, UDP
    网络层        ICMP, IP                            内核空间
    数据链路层     ARP, RARP, DataLink
    --------------------------------------------------

2. 封装 encapsulation
  TCP报文端，UDP报文端，MTU

3. 分用 demultiplexing
4. ARP: IP -> MAC
5. DNS: namespace -> IP, /etc/resolv.conf

第2章 IP协议
1. IPv4头部
![image](https://user-images.githubusercontent.com/22385430/161094882-a94e3f3b-d0af-461f-8870-80d0a95ebba2.png)

2. IP分片
3. IP路由
   计算下一跳路由
   查看路由表 netstat, route， 路由表更新 sudo route add(del)
4. IP转发
5. 重定向：ICMP重定向报文
![image](https://user-images.githubusercontent.com/22385430/161096241-ca75e1fc-6116-43a4-a921-f403fde8bc10.png)
6. IPv6头部
![image](https://user-images.githubusercontent.com/22385430/161096242-fb016d1c-47e6-4b0c-a1e6-b51748147221.png)

