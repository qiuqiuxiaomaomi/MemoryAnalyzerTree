# MemoryAnalyzerTree
内存分析技术研究

<pre>
[bonaparte@master bonaparte]$ jmap -heap 1299660
Attaching to process ID 1299660, please wait...
Debugger attached successfully.
   --服务端编译技术
Server compiler detected.
JVM version is 25.112-b15

using thread-local object allocation.
Parallel GC with 18 thread(s)

   --堆的配置信息
Heap Configuration:
   --最小堆使用比例
   MinHeapFreeRatio         = 0
   --最大堆使用比例
   MaxHeapFreeRatio         = 100
   --最大堆空间大小
   MaxHeapSize              = 16888365056 (16106.0MB)
   --新生代分配大小
   NewSize                  = 352321536 (336.0MB)
   --最大可分配新生代大小
   MaxNewSize               = 5629280256 (5368.5MB)
   --老年代大小
   OldSize                  = 704643072 (672.0MB)
   --新生代比例
   NewRatio                 = 2
   新生代与Survivor区比例
   SurvivorRatio            = 8
   --元数据区
   MetaspaceSize            = 21807104 (20.796875MB)
   CompressedClassSpaceSize = 1073741824 (1024.0MB)
   MaxMetaspaceSize         = 17592186044415 MB
   G1HeapRegionSize         = 0 (0.0MB)
   
   --堆的使用信息
Heap Usage:
   --年轻代
PS Young Generation
   --年轻代Eden区
Eden Space:
   capacity = 1760034816 (1678.5MB)
   used     = 1147281272 (1094.132682800293MB)
   free     = 612753544 (584.367317199707MB)
   65.18514642837611% used
   --年轻代幸存区FROM区
From Space:
   capacity = 22544384 (21.5MB)
   used     = 22362160 (21.326217651367188MB)
   free     = 182224 (0.1737823486328125MB)
   99.19171000635902% used
   --年轻代幸存区TO区
To Space:
   capacity = 66584576 (63.5MB)
   used     = 0 (0.0MB)
   free     = 66584576 (63.5MB)
   0.0% used
   --老年代
PS Old Generation
   capacity = 879755264 (839.0MB)
   used     = 96201360 (91.74476623535156MB)
   free     = 783553904 (747.2552337646484MB)
   10.935013854034752% used

33865 interned Strings occupying 3802480 bytes.
</pre>

![](https://i.imgur.com/CX8vIUM.png)

<pre>
堆的详细占用情况
[bonaparte@master]$ jmap -histo 1596579

 num     #instances         #bytes  class name
----------------------------------------------

</pre>

<pre>
GC日志输出

在jvm启动参数中加入
    -XX:+PrintGC -XX:+PrintGCDetails -XX:+PrintGCTimestamps -XX:+PrintGCApplicationStopedTime
jvm将会按照这些参数顺序输出gc概要信息，gc造成的应用暂停时间，
如果刚才的参数后面加入参数 -Xloggc：文件路径,
GC信息将会输出到指定的文件中。
</pre>

<pre>
jconsole
    jconsole是jdk自带的内存分析工具，他提供了图形界面。可以看到被监控的jvm的内存信息，线程
信息，类加载信息，MBEAN信息。
</pre>

<pre>
jstat
查询GC信息（1596579 为进程ID， 10000为每10s刷新一次）

[bonaparte@master ~]$ jstat -gcutil 1596579 10000
  S0     S1     E      O      M     CCS    YGC     YGCT    FGC    FGCT     GCT   
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
  0.00   0.00  40.92  11.36  98.03  96.95     11    0.328     3    0.473    0.800
</pre>

<pre>
top命令
   top命令是Linux下常用的性能分析工具，能够实时显示系统中各个进程的资源占用状况，类似于Windows的任务管理器

[bonaparte@master ~]$ top
top - 14:30:55 up 41 days, 16:21,  1 user,  load average: 0.29, 0.35, 0.39
Tasks: 572 total,   2 running, 568 sleeping,   0 stopped,   2 zombie
%Cpu(s):  2.2 us,  0.2 sy,  0.0 ni, 97.5 id,  0.0 wa,  0.0 hi,  0.1 si,  0.0 st
KiB Mem : 65966492 total,  2138232 free, 41765952 used, 22062308 buff/cache
KiB Swap: 33030140 total, 33030140 free,        0 used. 22329452 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                                                                                                                 
   7801 mysql     20   0 64.940g 0.019t   8368 S  10.6 30.5  15365:20 mysqld                                                                                                                  
1634771 apache    20   0  462092  21408   5280 S   9.9  0.0   0:01.26 httpd                                                                                                                   
1631721 apache    20   0  458940  18544   5312 S   8.6  0.0   0:17.07 httpd                                                                                                                   
1634307 apache    20   0  462624  22200   5288 S   8.6  0.0   0:02.23 httpd                                                                                                                   
1634258 apache    20   0  460812  20400   5296 S   7.9  0.0   0:03.00 httpd                                                                                                                   
1631278 apache    20   0  458172  17768   5304 S   2.6  0.0   0:19.57 httpd                                                                                                                   
1634824 apache    20   0  460832  20392   5272 S   2.6  0.0   0:00.38 httpd                                                                                                                   
1583737 bonaparte   20   0  397304  29352   5616 S   1.7  0.0   0:07.65 php-fpm                                                                                                                 
1312887 bonaparte   20   0  395256  27512   5660 S   1.3  0.0   0:54.81 php-fpm                                                                                                                 
     10 root      20   0       0      0      0 S   0.7  0.0 312:10.71 rcu_sched                                                                                                               
1215376 polkitd   20   0   50776  34144   1064 S   0.7  0.1 368:57.30 gitlab-unicorn-                                                                                                         
1634017 bonaparte   20   0  156208   2640   1508 R   0.7  0.0   0:01.01 top                                                                                                                     
3486631 polkitd   20   0 2736168 646932   9448 S   0.7  1.0  57:21.45 ruby                                                                                                                    
    593 root      20   0       0      0      0 S   0.3  0.0  61:21.83 xfsaild/dm-0                                                                                                            
   7308 root      20   0  231992  10140   4760 S   0.3  0.0   1:44.65 apache2                                                                                                                 
   8667 systemd+  20   0  501308   3688    732 S   0.3  0.0   6:18.15 zabbix_server                                                                                                           
   8682 systemd+  20   0  505084  10032   3256 S   0.3  0.0  18:41.83 zabbix_server                                                                                                           
1513274 bonaparte   20   0 21.968g 1.341g  13676 S   0.3  2.1  24:37.94 java                                                                                                                    
1624814 root      20   0       0      0      0 S   0.3  0.0   0:00.63 kworker/3:3                                                                                                             
1631110 root      20   0       0      0      0 S   0.3  0.0   0:00.21 kworker/5:1                                                                                                             
1634288 root      20   0       0      0      0 S   0.3  0.0   0:00.02 kworker/9:2                                                                                                             
1634769 root      20   0       0      0      0 S   0.3  0.0   0:00.01 kworker/10:2                                                                                                            
1821518 bonaparte   20   0 23.049g 975412  13704 S   0.3  1.5  73:19.42 java                                                                                                                    
      1 root      20   0  192436   5064   2148 S   0.0  0.0   7:00.04 systemd                                                                                                                 
      2 root      20   0       0      0      0 S   0.0  0.0   0:04.61 kthreadd                                                                                                                
      3 root      20   0       0      0      0 S   0.0  0.0  35:20.57 ksoftirqd/0     
</pre>

<pre>
free
在Linux下查看内存我们一般用free命令

[bonaparte@master ~]$ free
              total        used        free      shared  buff/cache   available
Mem:       65966492    41770156     2132956     1072636    22063380    22325160
Swap:      33030140           0    33030140
</pre>

<pre>
查询磁盘I/O情况

[bonaparte@master ~]$ iostat -x -k -d 1 2
Linux 3.10.0-693.2.2.el7.x86_64 (master.server.com) 	11/23/2018 	_x86_64_	(24 CPU)

Device:         rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
sda               0.00     0.18    5.44   42.79   103.39   901.55    41.68     0.16    3.40   14.05    2.04   0.90   4.34
dm-0              0.00     0.00    0.07    6.37     7.34    40.53    14.87     0.00    0.53    9.13    0.43   0.08   0.05
dm-1              0.00     0.00    0.00    0.00     0.00     0.00    46.25     0.00    7.35    7.35    0.00   4.48   0.00
dm-2              0.00     0.00    5.36   36.60    96.04   861.02    45.61     0.16    3.84   14.14    2.33   1.03   4.33
dm-3              0.00     0.00    0.16    4.31     8.51   108.02    52.12     0.01    1.73    3.56    1.67   0.08   0.04
dm-5              0.00     0.00    0.00    0.00     0.01     0.01    44.05     0.00   18.83   13.88   23.98   4.51   0.00
dm-6              0.00     0.00    0.00    0.30     0.02     3.05    20.64     0.00    0.42   50.72    0.24   0.21   0.01
dm-7              0.00     0.00    0.00    2.34     0.02    14.21    12.13     0.00    0.08   45.37    0.06   0.04   0.01
dm-10             0.00     0.00    0.14    0.33     8.20    20.67   123.90     0.01   16.07    1.43   22.09   0.24   0.01
dm-11             0.00     0.00    0.00    0.00     0.00     0.00    34.76     0.00   39.97   34.74  120.60  17.36   0.00
dm-8              0.00     0.00    0.01    0.01     0.09     0.19    30.84     0.00   19.11    8.43   28.10   2.92   0.01
dm-4              0.00     0.00    0.00    1.19     0.01    67.98   114.32     0.00    3.89    9.33    3.89   0.08   0.01
dm-9              0.00     0.00    0.00    0.01     0.02     0.20    45.59     0.00    0.87    5.05    0.59   0.62   0.00

</pre>

<pre>
查询磁盘使用情况

[bonaparte@master ~]$ df -h
Filesystem           Size  Used Avail Use% Mounted on
/dev/mapper/os-root   50G   32G   19G  64% /
devtmpfs              32G     0   32G   0% /dev
tmpfs                 32G  8.0K   32G   1% /dev/shm
tmpfs                 32G  930M   31G   3% /run
tmpfs                 32G     0   32G   0% /sys/fs/cgroup
/dev/sda2           1014M  123M  892M  13% /boot
/dev/mapper/os-data  2.7T  1.1T  1.6T  42% /data
tmpfs                6.3G     0  6.3G   0% /run/user/1000
tmpfs                6.3G     0  6.3G   0% /run/user/0
tmpfs                6.3G     0  6.3G   0% /run/user/1001
</pre>

![](https://i.imgur.com/bp9Yq6b.png)

![](https://i.imgur.com/0JHYvfh.png)

<pre>
JavaMissonControl

     随着JDK7 up40版本之后，jdk会自带JMC(JavaMissionControl)工具。可以分析本地应用以
     及连接远程ip使用。提供了实时分析线程、内存，CPU、GC等信息的可视化界面。从jdk8 up40
     开始，JMC还提供了在运行时创建JFR记录(飞行记录器)。如果是全面分析heap dump,再综合
     使用MAT(Eclipse Memory Analyzer)。基本就可以做很多日常的性能调优以及线上问题排查了。

     JMC是官方提供的免费工具，结合MAT，基本可以处理性能优化的80%场景。JMC还可以链接远程
     ip进行分析。但对于线上问题排查，还是建议使用jstat,jstack，jmap工具等，结合
     top、vmstat等快速排查和定位问题。 

     性能排查一般问题都集中在cpu、内存。前者分析线程，后者分析具体出现问题的内存分区。对于
     磁盘、IO等资源瓶颈需要综合很多业务场景进行具体定位。 
</pre>

