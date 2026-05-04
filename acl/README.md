## Acl(Access Control List)

# 一、ACL 是什么

Redis ACL（Access Control List）用于：

- 管理用户（username/password）
- 控制命令权限
- 控制 key 访问范围
- 替代旧的 `requirepass`

# 二、核心概念

## 1. 用户（User）

每个连接都是一个用户：

- 默认用户：`default`
- 可自定义：`appuser`, `readonly`, `admin`

## 2. 权限三要素

ACL 由三部分组成：

| 类型 | 说明               |
| ---- | ------------------ |
| 状态 | on / off           |
| 密码 | `>password`        |
| 权限 | 命令 + key pattern |

# 三、用户管理（最重要）

## 1. 创建用户

```
ACL SETUSER appuser on >pass123456 ~* +@all
```

含义：

- `on`：启用
- `>pass123456`：密码
- `~*`：所有 key
- `+@all`：所有命令

## 2. 查看用户

```
ACL LIST
```

查看单个用户：

```
ACL GETUSER appuser
```

## 3. 删除用户

```
ACL DELUSER appuser
```

------

## 4. 禁用用户（不删除）

```
ACL SETUSER appuser off
```

------

# 

# 七、持久化 ACL（重要）

保存配置：

```
ACL SAVE
```

或写入配置文件：

```
/etc/redis/users.acl
```

Redis 启动时加载：

```
aclfile /etc/redis/users.acl
```







## 一、标准 ACL 连接格式

```
redis://username:password@host:port/db
```


### 01 - Key

参数|说明
---|---
`~*` | 所有key
`~cache:*` |只能操作 `cache:*`

### 01 - Command

参数|说明
---|---
`+@all` | 允许所有命令（开发环境常用）
`+get +set +hget +hset` |只允许部分命令
