# LeetCode 189:轮转数组

<center>Author:ZeroOne</center>

## 问题：

给你一个数组，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。

示例 1:

```c
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```


示例 2:

```c
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```


提示：

```c
1 <= nums.length <= 105
-231 <= nums[i] <= 231 - 1
0 <= k <= 105
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/rotate-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



## 思路

这个问题有两种解答方法：双指针法和反转法。

##### 思路一：双指针法

轮转后的数组下标为`(i+k)%nums.length`，可以申请一个结果数组`result`来存放结果,这样只需要遍历一遍`nums`数组就能完成任务，复杂度为`O(n)`。

代码：

```c
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        vector<int> result(nums.size(), 0);
        int n = nums.size();
        for(int i=0; i<nums.size(); ++i)
            result[(i+k)%n] = nums[i];
        nums = result;
    }
};
```

##### 思路二：反转法

我们可以采用翻转的方式，比如12345经过翻转就变成了54321，这样已经做到了把前面的数字放到后面去，但是还没有完全达到我们的要求，比如，我们只需要把12放在后面去，目标数组就是34512，与54321对比发现我们就只需要在把分界线前后数组再进行翻转一次就可得到目标数组了。所以此题只需要采取三次翻转的方式就可以得到目标数组，首先翻转分界线前后数组，再整体翻转一次即可。

代码：

```c
class Solution {
public:
    void reverse(vector<int>& nums,int begin,int end)
    {
        int temp;
        while(begin<end){
            temp = nums[begin];
            nums[begin] = nums[end];
            nums[end] = temp;
            begin++;
            end--;
        }
    }
    void rotate(vector<int>& nums, int k) {
        if(nums.size()<2) return;
        k %=nums.size();
        reverse(nums,0,nums.size()-1);
        reverse(nums,0,k-1);
        reverse(nums,k,nums.size()-1);
    }
};
```



