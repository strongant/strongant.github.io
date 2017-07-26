title: Mac通过brew安装redis
author: strongant
tags:
  - mac
  - redis
  - brew
categories: []
date: 2017-07-26 21:41:00
---
## MacOS下通过brew安装redis

### 安装redis:

```
brew install redis
```
安装后的地址为:/usr/local/Cellar/redis/3.2.9

### 链接redis的launch开机启动配置文件
```
ln -sfv /usr/local/opt/redis/*.plist ~/Library/LaunchAgents
```

### 使用launchctl启动redis，每次开机启动
```
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.redis.plist
```

### 通过redis的配置文件进行启动
```
redis-server /usr/local/etc/redis.conf
```
### 停止开机启动redis

```
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.redis.plist
```

### 安装后的redis默认配置文件地址：
```
/usr/local/etc/redis.conf
```

### 卸载redis
```
brew uninstall redis
rm ~/Library/LaunchAgents/homebrew.mxcl.redis.plist
```

### 获取redis的安装信息
```
brew info redis
```

### 测试redis是否启动
```
redis-cli ping
```

如果redis返回“PONG”，那么说明连接成功






