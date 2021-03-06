# IPSec工作过程

## IPSec VPN分为两个协商阶段

IPSec VPN分为两个协商阶段，其实也是两个连接建立的阶段:

​        **管理连接**：IKE的SA的协商，分为主模式（Main mode）和积极模式(Aggressive mode)两种。主模式需要交互6个消息，而野蛮模式只需要交互3个消息；主模式协商比野蛮模式协商更严谨、更安全。第一个阶段IKE设置，有三个任务需要完成：	

1. 协商一系列算法和参数；（这些算法和参数用于保护隧道建立过程中的数据）必须计算出两边使用的加密KEY值；（DH算法）	
2. 对等体的验证，如何才能知道对端就是我要与之通信的对端。（设备验证）

​         **数据连接**：IPSEC的SA的协商 ，使用快速（Quick mode）模式。协商IPSec SA使用的安全参数，创建IPSec SA（SA可以加密两个对等体之间的数据，这才是真正的需要加密的用户数据），使用AH或ESP来加密IP数据流。至此IPSec VPN隧道才真正建立起来。

### 总结

1. 第一阶段作用：对等体之间彼此验证对方，并协商出IKE SA，保护第二阶段中IPSec SA协商过程；

2. 第二阶段作用：协商IPSec单向SA，为保护IP数据流而创建；
3. IKE的SA成功建立与否决定了IPSEC的SA是否能够成功建立

## 站点到站点的IPSec VPN建立的过程

1. 感兴趣的流通过

2. IKE的SA协商开始，协商如何保护管理连接

3. 运行DH算法协商出IKE的共享密钥

4. 在安全的管理连接上执行设备验证

5. IPSEC的SA协商开始：协商参数和密钥信息来保护数据连接（重新生成一个共享密钥）

6. 数据连接建立，加密传输数据

7. 管理和数据连接将会到期，并重新构建

