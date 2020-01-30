1、先安装一台有java虚拟机的服务器；
2、安装yum install wget
3、在home下创建一个文件夹soft，然后执行wget http://download.redis.io/releases/redis-5.0.7.tar.gz
4、然后在soft文件夹下解压tar xf redis-5.0.7.tar.gz
5、要安装redis需要安装gcc，有个gcc才有redis的编译环境，yum install gcc
6、准备就绪，就可以用make命令编译redis，安装redis。也可以用指定到目录下的安装方式，比如：make install PREFIX=/otp/redis5
7、进入vim /etc/profile目录，里面有个profile文件，把你的redis执行程序注册在里面，就跟java的javahome一样
export REDIS_HOME=/opt/redis5
export PATH=$PATH:$REDIS_HOME/bin
8、然后重新加载配置文件到内存 source /etc/profile，echo $PATH
9、src目录下有个执行文件redis-server。这个文件执行后redis启动，可是这是前端启动，如果ctrl+c就退出了，所以我们需要后台启动。
10、从readme得知，可以使用./install_server.sh可以启动，建议用这种方式启动redis。

Please select the redis port for this instance: [6379] 
Selecting default: 6379
Please select the redis config file name [/etc/redis/6379.conf] 
Selected default - /etc/redis/6379.conf
Please select the redis log file name [/var/log/redis_6379.log] 
Selected default - /var/log/redis_6379.log
Please select the data directory for this instance [/var/lib/redis/6379] 
Selected default - /var/lib/redis/6379
Please select the redis executable path [/opt/redis5/bin/redis-server] 
Selected config:
Port           : 6379
Config file    : /etc/redis/6379.conf
Log file       : /var/log/redis_6379.log
Data dir       : /var/lib/redis/6379
Executable     : /opt/redis5/bin/redis-server
Cli Executable : /opt/redis5/bin/redis-cli
Is this ok? Then press ENTER to go on or Ctrl-C to abort.

11：
  a）一个物理机可以有多个redis实例，端口号区分
  b）可执行程序就在一份目录，但是内存中多个实例，需要各自的配置文件，持久化目录等资源
  c）查看redis状态service redis_6379 status
  d）脚本还会帮你启动。

以上1-11步骤，redis在liunux环境安装完毕。

ps -fe | grep redis
