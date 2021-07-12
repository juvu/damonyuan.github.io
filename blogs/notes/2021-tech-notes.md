# 2021 Tech Notes

## [一台Linux服务器最多能支撑多少个TCP连接？](https://mp.weixin.qq.com/s/avJ9qXWHPhTNnOOzyYKWMA)

Key words:

- maximum file descriptors
  - 系统级
  - 用户级
  - 进程级
- 缓存区大小
  - net.ipv4.tcp_rmem  最小4K
  - net.ipv4.tcp_wmem  最小4K