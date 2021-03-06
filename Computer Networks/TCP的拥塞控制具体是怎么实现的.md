### TCP的拥塞控制具体是怎么实现的？
1. 慢开始：当 TCP 初次发送数据时，并不是直接发送大量的数据，而是先发送一小部分数据，然后将数据量逐渐增加，直到达到一个阈值（ ssthresh ）之后，数据量不再增加，之后进入拥塞避免状态。

  在 TCP 报文的头部有一个窗口大小字段，这个字段表示了当前端可以接受数据的缓冲区大小，拥塞窗口 cwnd 的值等于“接收端的窗口大小与发送端的窗口大小”两者之间较小的那一个。
  - 当 TCP 第一次建立连接的时候，cwnd=1 ，表示可以发送一个 SMMS （发送方的最大段大小）的大小
  - 每当发送端接收到一个接收端的 ACK ，cwnd 后面呈指数增长（2、4、8...）
  - 当 cwnd 达到一个阈值（ ssthresh ），cwnd 就不再呈指数增长了，而是进入拥塞避免阶段
    - 当 cnwd<ssthresh ，使用慢开始算法
    - 当 cnwd=ssthresh ，既可使用慢开始算法，也可以使用拥塞避免算法
    - 当 cnwd>ssthresh ，使用拥塞避免算法
2. 拥塞避免
当达到慢启动达到阈值之后，cwnd 就不再呈指数增长了，而是进入拥塞避免
- TCP 双方通信时，每经过一个往返时间RTT就将发送方的 cwnd+1 ，使 cwnd 呈线性增长
- 当 cwnd 一直增长，如果此时出现了丢包，那么就将阈值 ssthresh 减半，将 cwnd 重新置 1 ，下面又开始进入慢开始状态

乘法减小：无论是慢开始阶段还是拥塞避免，只要出现了网络拥塞（超时），就把慢开始门限值 ssthresh 减半

加法增大：执行拥塞避免算法后，拥塞窗口线性缓慢增大，防止网络过早出现拥塞
3. 快速重传
- 当发送端连续接收到 3 个“重复 ACK ”之后，说明有数据包丢失，立即重传，而不是等待超时重传计时器超时再重传
- 当有数据包丢失之后，不去启动“慢开始”算法，而是进入快速恢复
4. 快速恢复
- 发送方将慢开始中的 ssthresh 值和 cwnd 值调整为当前窗口的一半，然后下面开始执行拥塞避免算法
- 有的恢复算法会将 cwnd 增大一些，调整为新的 ssthresh
