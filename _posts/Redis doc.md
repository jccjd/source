---
date: 2019-09-13
tage:
- Redis
- docs
---
### 常用命令

**启动**

```bash
run redis : redis-cli redis-server
```
### 字符串

```bash
set key "this is key"

getrange key 0 -1
getrange key 0 3
mget
strlen
**getset**

返回给定 key 的旧值。 当 key 没有旧值时，即 key 不存在时，返回 nil 。
当 key 存在但不是字符串类型时，返回一个错误。
        getset db test
```
Redis可以被告知密钥应该只存在一段时间。这是通过EXPIRE和TTL命令完成的。


```bash
SET resource:lock "Redis Demo"
EXPIRE resource:lock 120
```
这会导致密钥资源：锁定在120秒内被删除。您可以使用TTL命令测试密钥的存在时间。它返回将被删除的秒数。


```bash
TTL resource:lock => 113
// after 113s
TTL resource:lock => -2
```
键的TTL的-2表示该键不再存在（不再）。一个-1的TTL钥匙意味着它永远不会过期。请注意，如果您设置了一个键，它的TTL将被重置。


```bash
SET resource:lock "Redis Demo 1"
EXPIRE resource:lock 120
TTL resource:lock => 119
SET resource:lock "Redis Demo 2"
TTL resource:lock => -1
```

##列表
    rpush friends 'bob'
    lrange friends 0 -1
    LPOP从列表中删除第一个元素并返回它。


```bash
LPOP friends => "Sam"
RPOP从列表中删除最后一个元素并将其返回。
RPOP friends => "Bob"
```

## 集合
```bash
sadd superpowers "flight"
sadd superpowers "x-ray vision"
sadd superpowers "reflexrs"

delete
srem superpowers "reflexrs"

find sismember
sismember superpowers 'flight' # 1
find al smembers
smembers superpowers #find all

合并 sunion
sadd birdpower 'pecking'
sadd birdpower 'flight'
sunion superpowers birdpowers

# 排序 1.2时引入
ZADD hackers 1940 "Alan Kay"
ZADD hackers 1906 "Grace Hopper"
ZADD hackers 1953 "Richard Stallman"
ZADD hackers 1965 "Yukihiro Matsumoto"
ZADD hackers 1916 "Claude Shannon"
ZADD hackers 1969 "Linus Torvalds"
ZADD hackers 1957 "Sophie Wilson"
ZADD hackers 1912 "Alan Turing"
zrange hackers 0 -1
```

### hash
```bash
hset user: 1000 name "john Smith"
hset user:1000 password "s3cret"
hset usert:1000 email "john.Smith@example.com"
hgetall user:1000
hget user:1000 name
```
