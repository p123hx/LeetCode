### 2267.Check-if-There-Is-a-Valid-Parentheses-String-Path

我们做过很多关于valid parentheses的题目。对于一个合法的括号字符串，必须满足两个条件：1. 任意的前缀字符串必须满足左括号的数目不能少于右括号的数目。2. 整个字符串结尾处，左右括号的数目必须相等。更具体的做法，就是用一个计数器count，来记录当前未被匹配的左括号的数量，一定在从左往右遍历的过程中发现count小于0，那么即可判定该字符串不可能是valid parentheses.

本题形式上非常类似常规的“走迷宫”型DP。事实上，也确实是同样的套路。我们想用dp[i][j]表示某个字符串路径到达(i,j)时是否依然合法，必然需要记录的就是未被匹配的左括号数量。但是由于之前路径的不同，到达(i,j)时的未匹配左括号的数量也必然可能有多个，所以本题里dp[i][j]其实是一个集合。

dp[i][j]的前驱状态有两个，dp[i-1][j]和dp[i][j-1]. 假设前驱状态的两个集合总共包含了{0,2,3}，并且(i,j)是一个左括号，那么dp[i][j]就可以是{1,3,4}，也就是将前者集合的元素都增1. 相反地，如果(i,j)是一个右括号，那么需要和之前的左括号对消，故dp[i][j]就是{1,2}. 特别注意，d[i][j]里面不能加入-1，因为不会有valid parentheses里面（哪怕是暂时地）出现未匹配的左括号是负数。

特别地，如果dp[i][j]的前驱状态的集合是空集，那么意味着无论如何，从起点到(i,j)都不会有合法的路径，故dp[i][j]也必须赋值为空集。

另外，本题有一个剪枝的技巧。因为路径的步长是固定，当我们走完一定步数之后，发现剩下未走的步数就算都看做是右括号，也无法抵消当前剩余的左括号的话，那么注定这条路径是不能成功的，就可以提前终止。

最终的答案就是查看dp[m-1][n-1]这个集合是否包含零元素。
