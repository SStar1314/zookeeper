ZooKeeper3.4版本基本上玩的可以了，包括：Server，Client，RestAPI。使用，部署，源代码都看过，详细纪录存在印象笔记里面，可以查看。
关于recipes这部分内容相对比较复杂，目前看代码意义不大，暂时先搁置一边。

任何一个分布式协同管理平台系统无法同时满足CAP特性，ZooKeeper应该是做到了ZP。
CAP定理（C-数据一致性；A-服务可用性；P-服务对网络分区故障的容错性）


这是我的本地版本：
请查看branch-3.4分支，我有一些纪录



For the latest information about Apache ZooKeeper, please visit our website at:

   http://zookeeper.apache.org/

and our wiki, at:

   https://cwiki.apache.org/confluence/display/ZOOKEEPER

Full documentation for this release can also be found in docs/index.html

---------------------------
Packaging/release artifacts

The release artifact contains the following jar file at the top level:

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
The contents of the legacy jar and the bin + sources jars are the same.





As of version 3.3.0, the bin, sources and javadoc jars contained in the
dist-maven directory are deployed to the central repository after the release
is voted on and approved by the Apache ZooKeeper PMC:

  https://repo1.maven.org/maven2/org/apache/zookeeper/zookeeper/
