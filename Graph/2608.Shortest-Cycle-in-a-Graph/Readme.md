### 2608.Shortest-Cycle-in-a-Graph

这是图论里的经典问题。解法非常简单，就是遍历所有的边`a-b`。查看如果将该边断开，从a到b的最短距离d，那么d+1就是就包含d的最短环。然后取全局的最小值即可。
