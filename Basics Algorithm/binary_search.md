# Binary Search - 二分搜索

二分搜索是一种在有序数组中寻找目标值的经典方法，也就是说使用前提是【有序数组】。非常简单的题中【有序】特征非常明显，但更多时候可能需要我们自己取构造【有序数组】。下面从最基本的二分搜索开始逐步深入。

## 模版一　- lower/upper bound

定义lower bound为给定升序数组中大于等于目标值的最小索引，upper bound则为小于等于目标值的最大索引

```python
class Main(object):
    def __init__(self):
        pass
    
    def lowerBound(self, nums, target):
        if not nums or len(nums) == 0:
            return -1
        lb, ub = -1, len(nums)
        while lb + 1 < ub:
            mid = lb + (ub - lb) // 2
            if nums[mid] < target:
                lb = mid
            else:
                ub = mid
        
        return lb+1
   
	def upperBound(self, nums, target):
        if not nums or len(nums) == 0:
            return -1
        lb, ub = -1, len(nums)
        while lb + 1 < ub:
            mid = lb + (ub - lb) // 2
            if nums[mid] > target:
                ub = mid
            else:
                lb = mid
        return ub - 1
    
```

###　源码分析

以`lowerBound`的实现为例：

１．while 循环中`lb+1 < ub`，最后循环退出时一定有`lb+1==ub`

２．`mid = lb + (ub - lb) // 2`，可有效防止两数相加后溢出

３．`lb`和`ub`的初始化，初始化为数组的两端之外，这种初始化方式比起`0`和`len(nums)-1`有不少优点。详述如下：

​	１．目标值在数组范围之内，最后返回值一定是`lb+1`

​	２．目标值比最小值还小时，此时 lb 一直是 -1，故最后返回 lb + 1也没错

​	３．目标值大于数组最后一个值，循环退出时一定有 lb = len(nums) - 1，应该返回 lb + 1

**个人认为可以这样理解上述模版算法，lb与ub之间的元素都会在二分搜索的算法之下判断，唯独lb与ub对应的元素不会由二分搜索判断（二分搜索不会判断lb与ub的元素是否与target相同），故 lb = -1，ub = len(nums)是十分合理的**

## 模版二 - 最优解

除了在有序数组中寻找目标值这种非常直接的二分搜索外，我们还可以利用二分搜索求最优解（最大值/最小值），通常这种题只是隐含了【有序数组】，需要我们自己构造。

用数学语言来描述就是【求满足某条件C(x)的最大/小的x】，以求最小值为例，对于任意满足条件的$x^`$,如果存在$x<= x^` <=UB$, 且$x$也满足条件，（其中UB可能是无穷大，也可能是满足条件的最大解），那么$x$就是最小解。

那么我们就能用二分搜索求解。好好理解下面这道题

### Problem Statement

有N条绳子，它们的长度分别为$L_i$，如果从它们中切割出K条长度相同的绳子，这K条绳子每条最长能有多长？答案保留到小数点后两位。

**输入**

`N = 4，L = {8.02，7.43，4.57，5.39}，K=11`

输出

`2.00`

### 题解

这道题看似是一个最优化问题，我们尝试使用模版二的思想求解，**令$C(x)$为【可以得到K条长度为x的绳子】**，根据题意，我们可以将上述条件进一步细化为：

$C(x) = \sum_{i}(floor(L_i/x)) \ge K$

我们现在来分析可行的上下界，显然绳子长度一定大于０，大于０的小数点后保留两位的最小值为0.01，显然如果最后有解，0.01一定是可行解中最小的，且这个解可以分割出的绳子条数是最多的。一般在 OJ 上不同变量都是会给出范围限制，那么我们将上界初始化为`最大范围 + 0.01`, 它一定在可行解之外（也可以遍历一遍数组取数组最大值，但其实二分后复杂度相差不大）。使用二分搜索后最后返回`lb` 即可。

**个人感觉上面这一段的作用就是找大于最大可能解的值，以及小于最小可能解的值。就好比上面的令lb=-1，ub=len(nums)，-1是比最小可能解还小，len(nums)是比最大可能解还大，这样的话，lb与ub之间的值都会由二分搜索判断，而lb与ub之间则正好为所有可能的解。**

#### python

```python
class Main(object):
    def __init__(self):
        pass
    
    def solve(nums, K):
        lb, ub = 0.01, 10e5 + 0.01
        # while lb + 0.001 < ub:
        for i in range(100):
            mid = lb + (ub - lb) / 2
            if C(nums, mid, K):
                lb = mid
            else:
				ub = mid
         return lb
    
    def C(nums, seg, K):
        count = 0
        for num in nums:
            count += num // seg
        return count >= K
```

#### 源码分析　

方法`C`只做一件事，给定数组`nums`，判断能否切割出`K`条长度均为`seg`的绳子。`while`循环中使用`lb + 0.001 < ub`，不能使用`0.01`，因为计算mid时有均值的计算，会造成较大的误差。

## 模版三 - 二分搜索的`while`结束条件判定

对于整型我们通常使用`lb + 1 < ub`，但对于`double`型数据来说会有些精度上的丢失，使得结束条件不是那么好确定。像上题中采用的方法是题目中使用的精度除10。但有时这种精度可能还是不够，但是如果结束条件`lb + EPS < ub`中使用的EPS过小时double型数据精度有可能不够从而导致死循环的产生！这时候我们将`while`循环体替换为`for i in range(100)`，100次循环后可以达到$10^{-30}$精度范围，一般都没问题。

