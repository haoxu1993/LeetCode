### 42. Trapping Rain Water 

#### 解法1：考虑每个位置的上方可以存多少水

此题巧妙的解法是找到解析式来表达位置i可以存多少水：
```cpp
area[i]=min(LeftMost[i]+RightMost[i])-height[i];
area[i]=area[i]<0?0:area[i];
```
LeftMost[i]是指i左边的最大高度：
```cpp
LeftMost[i]=max(LeftMost[i-1],height[i-1]);
```
RightMost[i]的定义同理。

#### 解法2：考虑每个位置的上方构成的最大矩阵

这种解法和```084.Largest-Rectangle-in-Histogram```正好相反。那题是维护一个递增栈，如果遇到一个矮的bar，那么我们就可以分割出一块以栈顶元素为高的矩形，宽度取决于栈顶元素之前的元素位置（次栈顶元素）和之后的元素位置（也就是最新的bar）。

这题正好相反的概念。我们维护一个递减栈。如果遇到一个高的bar，那么以栈顶元素为洼地可以分割出一块蓄水矩形，其高度取决于栈顶元素左右两边的高度的较矮值，其宽度取决于栈顶元素之前之后的位置。比如说 [7,4,3,2,1,6]:

当考察6的时候，考虑1这个洼地，可以蓄水的面积就是```高=min(2,6)-1, 宽=5-3-1```. 然后弹出1. 接下来考察2这个洼地，可以蓄水的面积是```高=min(3,6)-1, 宽=5-2-1```。注意洼地2对应的蓄水矩形在横向上是覆盖了1的，但是面积并不包括之前洼地1所算的矩形。

以此类推，6可以将1,2,3,4都一次弹出。然后6就可以入栈。此时栈仍然是单调减的。

把所有洼地对应的矩形都加起来就是答案。

[Leetcode Link](https://leetcode.com/problems/trapping-rain-water)
