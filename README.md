# daily
日常记录
===============================
  10-26：
>Redis：存放在内存的
-------------------------
### 基本数据类型操作
  * #### `String` 
    * `set` a 1 
    * `get` a  
    * `incr` b  ###加1，不存在的话会创建这个变量
    * `decr` b   
  * #### `Hash`
    * `hset` hash1 a 1  ###hash1是HashName，a是key
    * `hget` hash1 a
  * #### `List`
    * `lpush` list1 a b c d ###不断的向左边添加数据
    * `lrang` list1 ###d c b a
    * `rpush` list1 1 2 3 4 ###向右边添加数据
    * `lrang` list1 ###d c b a 1 2 3 4
    * `lpop` list ###去掉最左边、c b a 1 2 3 4
    * `rpop` list ###去掉最右边、c b a 1 2 3 
  * #### `set` ###去重，无序
    * `sadd` set1 a b c c c d 
    * `smembers` set1
### key命令
###设置key过期时间：hash1、list1、set1<br>
  * `expire` hash1 60        ###设置hash1的过期时间为60s
  * `ttl` hash1              ###查询过期时间
  * `expire` hash1 60        ###重置key的过期时间
  * `persist` hash1          ###清除过期时间
### Redis快照
  * rdb：定期备份数据到磁盘上
  * aof：把所有对Redis的操作命令保存到文件中，每秒作一次同步，数据库恢复的时候执行一次文件即可
### Redis集群
  * 集群管理机制：使用投票机制、超过半数的认为该服务器不能用了
  * 对于内容的存储算法：Redis内置16384个槽、把集群中的Redis服务器分配对应的槽位、当放置一个key的时候需要通过对应的算法放置到对应的槽位、也就是放置
    到对应的Redis服务器.
  * 集群至少需要３台服务器，这样投票才能超过半数，每一台ｒｅｄｉｓ都需要一个备份机，那么至少需要６台服务器
  * 在一台虚拟机上配置６台redis，通过端口来区分
    * 复制６个/usr/local/redis/bin目录
      * 创建一个新的目录　mkdir /usr/local/redis-cluster
      * cp /usr/local/redis/bin /usr/local/redis-cluster/redis-01  ###只是把bin的名字改为redis-01,操作６次
      * 复制/home/lzx/redis/bin/redis.conf 复制到redis-01下，修改port 7006、cluster-enable yes、daemonize yes
      * 在redis-cluster下创建start-redis-cluster.sh文件启动六个redis
      * cp /home/lzx/redis/redis-trib.rb /usr/local/redis-cluster ###复制rb文件
      * 执行配置ｒｂ文件
      
### Redis同步
  * 其实在做增删改的时候删除对应的缓存、这样下次获取数据的时候就能更新缓存
### Linux安装Redis
  * 下载tar.gz压缩包、解压tar zxvf redis-3.0.0.tar.gz
  * yum install gcc-c++安装c的编译环境
  * make 编译
  * make install PREFIX=/usr/local/redsi 把安装成功的文件放置到redis目录下、redis-server和redis-cli
  * 进入redis启动redis，使用后端启动模式
    * cd /home/lzx/redis 找到redis.conf
    * cp redis.conf /usr/local/redis/bin 复制到安装目录下
    * vim /usr/local/redis/bin/redis.conf 修改daemonize为yes
    * cd /usr/local/redis/bin
    * ./redis-server redis-conf       启动redis
    * ps aux | grep redis  查看是否启动成功
    * kill 11199 
    * ./redis-cli 启动界面
 >Solr
-------------------------
### Solr集群:Solr Cloud
  * 由于限制Tomcat的链接限制，所以在高并发、可扩容的场景下需要集群．使用Solr和Zookeeper来搭建Solr Cloud. 
  * 海量存储：
    * 在逻辑上把存储的内容分隔为多个块，每个块放置每一个solr下的一个片中、有一个solr中的片作为主节点、其他是备份节点、这样实现海量存储．
  * 高并发：
    * 在上面的分隔结果上、主从节点一起工作实现高并发处理
### ActiveMQ: 实现系统间（不同功能模块之间的调用）、实现解耦．
  * 点到点通信：一个提供者一个消费者
  * 订阅模式：
  
