### 2508.Add-Edges-to-Make-Degrees-of-All-Nodes-Even

本题没有特别的，就是考虑对图的几何分析。令度为奇数的点的数目为m，分情况讨论：

如果m等于1，那么任何新连接到m的边，都会破坏另一个节点度的偶性。

如果m等于2，那么(1) 如果这两点之间没有边，那么就一条边将其相邻即可。(2) 如果这两点a,b之间已经有边，那么我们需要令找一个（度为偶数）的点c，且该点ac和bc都能再连一条边。

如果m等于3，我们无法用两条边，仅改变这三个点的度的奇性。

如果m等于4，我们令其为a,b,c,d。只有ab、cd可连边，或者ac、bd可连边，或者ad、bc可连边，三种情况能符合要求。

如果m大于等于5，我们无法用两条边连到5个或更多的点（改变它们的度），返回false。
