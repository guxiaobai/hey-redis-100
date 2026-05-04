## Hey Redis 100

检查版本

```
redis-cli info
```

## 链接

```bash
redis-cli -u redis://appuser:pass123456@192.168.1.100:6379/0
redis-cli -h 192.168.1.100 -p 6379 -u redis://appuser:pass123456
```

## 安装

```bash
apt-get install -y redis-server redis-tools
sudo systemctl stop redis.service
sudo systemctl restart redis

# 使用官方安装源
systemctl status redis-server.service 
```

## 配置

> `/etc/redis/redis.conf`

```
bind 127.0.0.1 192.168.100.63

protected-mode no
requirepass password
```



```
redis://192.168.100.63:6379/0
```



> 远程机器连接测试

```bash
redis-cli -h 你的服务器IP -p 6379
auth yourpassword
```

## Ref

- <https://redis.io/open-source/>
- <https://valkey.io/>