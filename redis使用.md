理论：
1、yum install man man-pages。先安装这个帮助程序，cd /proc/12952/fd看redis的详细进程，基于文件描述符

BIO每个线程hold住一个任务，而且堵塞，有更多的线程完成多任务；如果是NIO可以一个线程hold多个任务，因为非堵塞
