### 1066.Campus-Bikes-II

此题是著名的带权二分图的最优匹配问题，可由KM算法解决。在这里，因为数据量比较小，我们通常可以用状态压缩DP，或者基于状压的最小路径问题来解决。类似的题目还有1879,1947

#### DP
我们令m是自行车的数量，n是人的数量。我们通常会约定，按人的先后顺序依次挑自行车（因为人的数量少于自行车，每个人一定能配对自行车；反之不成立）。

我们将“自行车被选取的状态”作为节点，比如```state = 1001010```表示第0、3、5号自行车被配对。特别注意，因为我们约定了工人按顺序挑自行车，所以这三辆自行车一定是被前3号工人调走的。我们想要求该状态的最优解dp[state]（即实现该状态对应的最小配对代价），突破口就是最后一个人（即第2号工人）挑选的是其中的哪一辆。例如，上面的例子里，我们分别遍历第0,3,5好自行车与第2号工人配对的可能，即state的前驱状态就有```001010, 1000010,1001000```三种。所以状态转移方程就是
```
dp[state] = min{dp[state - (1<<i)] + dist[i][j]} for all i where the i-th bit of state is 1
```
其中j可以由state确定。假设state里含有3个1 bit，说明有三辆自行车被匹配，对应的是前3号工人，那么j就是最后一个已配对工人的编号2。

#### Dijsktra
我们将“自行车被选取的状态”作为节点，状态之间的跳转理解为节点之间的相邻关系，状态之间的权重差就是相邻边的权重，就可以用Dijkstra算法了。举个例子，状态0110表示前两个工人（0号和1号）已经被配对1号和2号自行车的最优价值（即最小的配对距离之和）。注意，这个状态中我们不再区分前两个工人分别配对了哪辆自行车，我们不关心，我们只关心前两个工人的总和状态。状态0110可以转移到另外两种状态：如果2号工人选择0号自行车，即转移到了1110，权重的变化就是dist[2][2]；如果2号工人选择3号自行车，即转移到了0111，权重的变化就是dist[3][2]。

我们的起点是全为0的state，终点是一个包含m个1（工人数目）的state，求其最短路径。至此，我们已经完全把这道题转化为了Dijkstra的模板了。BFS+PQ利用贪心法的思想就可以很容易解决：利用优先队列来进行BFS搜索，所有状态在队列里按照cost从小到大排序。如果某个状态第一次被PQ弹出，那么它对应的cost就是实现该状态的最优解。


[Leetcode Link](https://leetcode.com/problems/campus-bikes-ii)