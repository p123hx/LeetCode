### 2417.Closest-Fair-Integer

为了寻找最小的答案，我们尽量保持高位不变。假设“仅”令前k-1位不变，如何构造一个比n稍微大一点的数呢？

显然将第k位增加1，后面剩余的位数置零（假设有count个），这就是最小的方案了。此时我们基于这个新数num，用一个函数`helper(num,count)`来寻找最接近的答案：如果此时前k位的digit的奇偶个数之差是diff，那么这个diff可以由后面count位来抵消，怎么抵消呢，显然应该从count拿出一部分置为1，一部分置为0，其中将所有的1放在末尾即可。于是，简单的“和差问题”即可求出最后的count位里需要填充多少个0和多少1能够满足条件。注意，也有可能无解。

如果无解，我们需要尝试将第k位为增加2，继续调用之前的`helper(num,count)`。

如果依然无解，那么不需要再增加第k位的数字了，因为增加3对于前k位的奇偶数字数目不会带来变化，等同于第一种情况。于是我们应该减少k，即“仅”保持前k-2位不变，再重复之前的步骤。

最终本题一定有解。

注意，我们首先要检查原数n本身是否是符合条件的。
