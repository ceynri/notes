# Flex 布局详解

flex-grow 作用的是**剩余**空间，所以当元素都占据一定空间的时候flex-grow看起来会失效。

解决方法：如果需要几个元素等分某个区域，则给每个div设置`width: 0`，然后再分配flex-grow