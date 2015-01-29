做这道题之前，我觉得应该回顾一下[33. Container With Most Water](../33. Container With Most Water)，两道题属于同一种类型。

既然同类题，也甭管什么 Hard 难度了，照样一个循环搞定。

思路如下：

```cpp
               _
       _      |@|_   _
   _  |@|_   _|@| |_|@|_
 _|@|_|@| |_| |@| | |@| |
 0 1 0 2 1 0 1 3 2 1 2 1  
     *   * * *     *
           *
// 这道题乍一看没啥思路，但我们可以看出一个很显然的规律：水肯定是夹在坑里的。
// 你至少有个坑对吗？我用 @ 标识出了例子数据中的坑，需要思考一个问题，中间那个 101 为何不是坑？
// 显然，因为山外有山，坑外有坑，只有最外，最大的那个坑才对我们来说有意义。
// 结合 33 题，我们应该有一个思路，就是 “夹逼法”。设置:

int i=0, j=n-1; // 一首一尾
int maxI = A[i], maxJ = A[j]; // 坑的外壁，很显然是 “往里走， 遇大替”

if (maxI < maxJ) // 左头小于右头，故移左头。
    ++i;
else             // 反之，移动右头。
    ++j;
```

为何移动小的那个？想象一下坑是啥样子，必须是两头高耸嘛，再看下图：

```cpp
 _                     _
| |_   _         _   _| |
| | |_| |_ and _| |_| | |
 ^       ^     ^       ^
// 你移动左边还是移动右边？答案是非常显然的。
```

光是移动不行，我们在移动过程中要记录两件事：

1. 时刻保证坑壁的最大性
2. 累计坑面积（咱们的返回值）

对于1，简单：
```cpp
maxI = max(maxI, A[i]), maxJ = max(maxJ, A[j]);
```
对于2，一句话：如果遇到下坡，即进坑，则累计坑深度。
```cpp
count += maxI - A[i];
count += maxJ - A[j];
```

这样，答案呼之欲出了吧。