### 2484.Count-Palindromic-Subsequences

长度为5的回文串，意味着我们对中间的字符没有任何要求。剩下的镜像部分，本质只是两个字符的组合。考虑到本题的元素只是数字，只有0-9共10种可能，所以组合的方式只有100种。结合字符串的长度是1e4，基本可以判定时间复杂度就是10^6，状态变量定义为`dp1[i][j][k]`表示前i个元素的子串里，以j和k结尾的subsequence有多少。同理定义为`dp2[i][j][k]`表示后i个元素逆序来看的子串里，以j和k结尾的subsequence有多少。这样我们枚举长度为5的回文串的中间字符位置i，则有`ret+=dp[i-1][j][k]*dp[i+1][j][k]`.

接下来考虑`dp1[i][j][k]`如何求解。依然从第i个元素下手。如果第i个元素没有贡献任何“以j,k结尾的新子串”，则有`dp1[i][j][k] += dp[i-1][j][k]`。如果第i个元素恰好是k，那么s[i]本身就可能贡献一个“以j,k结尾的新子串”，这个子串的数目取决于i之前出现了多少个j。所以我们还需要预处理得到一个`count1[i-1][j]`表示前i-1个元素里面有多少个j。因此就有`dp1[i][j][k] += count1[i-1][j]`.

同理我们可以逆序处理得到count2和dp2.
