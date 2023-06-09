### 2401.Longest-Nice-Subarray

本题的本质就是找一段最长区间，使得这个区间内每个bit位上最多只出现一个1. 这其实就是和`003.Longest-Substring-Without-Repeating-Character`一样的思想。

我们可以开一个长度为32的数组来记录每个bit位上出现1的频次，但是更精彩的做法就是用一个二进制数count本身来记录。count的每个bit可以记录该位置出现了0次或者1次的1。只要`(count & nums[j])==0`，那么意味着没有任何一个bit位上的1出现了超过1次，于是滑窗的右边界就可以不断右移。反之，就意味着不能继续右移，那么此时`[i,j-1]`就是以i开头的、符合条件的最长区间。接下来我们只要移动左指针i，将nums[i]从count里移出，那么就可以继续尝试移动右指针了。
