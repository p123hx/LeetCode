### 2381.Shifting-Letters-II

这是一道非常明显考察差分数组的题目。我们维护一个差分数组diff[i]表示从i开始之后的每一个元素将如何变化。如果对于区间[a,b]内的字符都要增1，那么我们只需要记```diff[a]+=1, diff[b+1]-=1```.我们将所有的区间都用diff处理之后，再从前往后计算diff的前缀和，所得的`delta[i] = sum(diff[0:i])`就是表示第i个字符最终累积要增加（或者减少）的数目。

特别注意，presum_diff[i]可能非常大，需要对26取余，并且我们需要保证是正数，且`s[i]+delta[i]`要折算到[0,25]之内。
