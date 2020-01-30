1、src目录下有个执行文件redis-server。这个文件执行后redis启动，可是这是前端启动，如果ctrl+c就退出了，所以我们需要后台启动。
2、从readme得知，可以使用./install_server.sh可以启动，建议用这种方式启动redis。

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
