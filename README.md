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
   MinHeapFreeRatio         = 0
   MaxHeapFreeRatio         = 100
   MaxHeapSize              = 16888365056 (16106.0MB)
   NewSize                  = 352321536 (336.0MB)
   MaxNewSize               = 5629280256 (5368.5MB)
   OldSize                  = 704643072 (672.0MB)
   NewRatio                 = 2
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