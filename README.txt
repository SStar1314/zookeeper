For the latest information about ZooKeeper, please visit our website at:

   http://zookeeper.apache.org/

and our wiki, at:

   https://cwiki.apache.org/confluence/display/ZOOKEEPER

Full documentation for this release can also be found in docs/index.html

---------------------------
Packaging/release artifacts

The release artifact contains the following jar file at the toplevel:

zookeeper-<version>.jar         - legacy jar file which contains all classes
                                  and source files. Prior to version 3.3.0 this
                                  was the only jar file available. It has the 
                                  benefit of having the source included (for
                                  debugging purposes) however is also larger as
                                  a result

The release artifact contains the following jar files in "dist-maven" directory:

zookeeper-<version>.jar         - bin (binary) jar - contains only class (*.class) files
zookeeper-<version>-sources.jar - contains only src (*.java) files
zookeeper-<version>-javadoc.jar - contains only javadoc files

These bin/src/javadoc jars were added specifically to support Maven/Ivy which have 
the ability to pull these down automatically as part of your build process. 
The content of the legacy jar and the bin+sources jar are the same.

As of version 3.3.0 bin/sources/javadoc jars contained in dist-maven directory
are deployed to the Apache Maven repository after the release has been accepted
by Apache:
  http://people.apache.org/repo/m2-ibiblio-rsync-repository/



《ZooKeeper分布式过程协同技术详解》这本书比较赞，提到了几篇文章：
1.Impossibility of Distributed Consensus with One Faulty Process
2.Brewer’s Conjecture and the Feasibility of Consistent, Available, Partition-Tolerant Web Services.
3.The Part-Time Parliament.
4.Exploiting Virtual Synchrony in Distributed Systems.

ZooKeeper Service:

ZooKeeper Namespace:

ZooKeeper API:
1.create /path data
2.delete /path
3.exists /path
4.setData /path data
5.getData /path
6.getChildren /path

ZooKeeper znode类型:
1.持久节点persistent node: 持久的znode只能通过delete来进行删除。
2.临时节点ephemeral node: 当创建znode的客户端关闭连接时，改节点就会被删除。
3.有序节点sequential node: 有序持久节点，有序临时节点。znode- 会自动分配序列

轮询 vs 通知(Notification)：《ZooKeeper分布式过程协同技术详解》书中详细的介绍了轮询和通知的流程，ZooKeeper采用了notification的形势，Watcher是ZooKeeper的重要内容。

ZooKeeper服务器的两种工作模式： 独立模式(standalone)和仲裁模式(quorum)
独立模式(standalone): 单独的ZooKeeper服务器。
仲裁模式(quorum): ZooKeeper集合(ZooKeeper ensemble)。 仲裁模式中，为减少ZooKeeper Server数据同步的延迟，法定人数 的概念被使用，法定人数的大小设置非常重要。

会话(Session)，会话状态：NOT_CONNECTED, CONNECTING, CONNECTED, CLOSED.
启动ZooKeeper服务：bin/zkServer.sh start
客户端发起会话连接：bin/zkCli.sh

zxid: 事务标志符。

仲裁模式试验：
configure 文件：
z1.cfg
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/root/zookeeper-3.4.8/conf/z1/data
clientPort=2181
server.1=127.0.0.1:2222:2223
server.2=127.0.0.1:3333:3334
server.3=127.0.0.1:4444:4445
z2.cfg
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/root/zookeeper-3.4.8/conf/z2/data
clientPort=2182
server.1=127.0.0.1:2222:2223
server.2=127.0.0.1:3333:3334
server.3=127.0.0.1:4444:4445
z3.cfg
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/root/zookeeper-3.4.8/conf/z3/data
clientPort=2183
server.1=127.0.0.1:2222:2223
server.2=127.0.0.1:3333:3334
server.3=127.0.0.1:4444:4445
启动服务命令：
/root/zookeeper-3.4.8/bin/zkServer.sh  start  z1/z1.cfg
/root/zookeeper-3.4.8/bin/zkServer.sh  start  z2/z2.cfg
/root/zookeeper-3.4.8/bin/zkServer.sh  start  z3/z3.cfg
连接集群：
/bin/zkCli.sh -server 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183
创建ephemeral 节点：
create -e /master "master.example.com"
创建sequential 节点：
create -s /master/task-  “cmd"

WatchedEvent 数据结构包含以下信息：
ZooKeeper会话状态(KeeperState)：Disconnected, SyncConnected, AuthFailed, ConnectedReadOnly, SaslAuthenticated, Expired.
事件类型(EventType)：NodeCreated, NodeDeleted, NodeDataChanged, NodeChildrenChanged, None.
如果事件类型不是None时，返回一个znode路径.
监视点设置：
NodeCreated：通过exists调用设置监视点。
NodeDeleted：通过exists或getData调用设置监视点。
NodeDataChanged：通过exists或getData调用设置监视点。
NodeChildrenChanged：通过getChildren调用设置监视点。








