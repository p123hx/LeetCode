### 2421.Number-of-Good-Paths

#### 方法1：并查集
我们看到元素个数是`3e4`，并不是特别好判断对于时间复杂度的要求。但是注意到数值大小的范围是1e5，这就提醒我们可以从数值大小出发。我们不妨尝试从小到大分析这些节点。

首先考虑数值为0的节点。多数情况下，它们应该都是离散的点。但是有些时候一些0节点是彼此联通的，那么在这个联通区间内，任意两个节点都是一条合法的path（因为经过的任意节点都是0）。

此时我们再考虑数值为1的节点。因为我们此时仅考虑数值是0或1的节点，我们仅限引入那些以1为一个端点、以0或1为另一个端点的边。加入这些边后，那么就可以拓展上面的联通区域。并且我们可以发现，在每个联通区域内，任意两个以1节点为端点的path都是合法的。我们只需要知道此时这些1节点在各自联通区域内的分布数量，就可以算出有多少个这样的path。

接下来我们在考虑数值为2的节点。类似地，我们引入所有端点数值不超过2的边，进一步扩展上述的图，有些区域会被进一步联通。在每个联通区域内，任意两个以2节点为端点的path都是合法的。

可见，这道题的算法就是并查集，从小到大地引入节点（和相应的边），构建联通关系。

为了操作上的方便，我们将所有的edge按照较大的端点分类。比如说e[2]，表示所有以（数值）2节点为一端，以0/1/2节点为另一端的边的集合。这样方便我们按顺序往图里加入边。

#### 方法2：DFS
本题其实也可以按照普通的DFS来做。我们任意以某个节点（比如说0号节点）为根，看做一棵rooted tree. 类似于“path in a tree”的思想，对于每个节点node而言，我们想知道以它为turning point的合法path有多少（每个path必然有一个turning point和两条单链）。以此做不重不漏的统计。

考虑对于node作为turning point的合法路径。假设其端点数值是x（显然x必须大于等于vals[node]），我们只需要知道每个子树里有多少条以x为端点、node为终点的合法单链（该单链里任何元素都不大于x）。将这些不同子树的这些单链之间彼此组合即可。

更具体地，对于每个node，我们设计一个数据结构`map<int,int> count`，其中key表示子树里节点的数值，val表示该数值的节点（可能有多个）到node的合法单链的数目（合法的意思是沿途的节点数值都小于key）。显然，为了保证单链的合法性，我们只需要在map里保存其中key值大于等于vals[node]的部分。对于node的每个孩子的递归结果`map<int,int> tmp`，我们最终都要将其merge到node的count里去。在merge前，对于tmp里的每一个key，都有`ans+=tmp[key]*count[key]`；在merge后，对于tmp里的每一个key，都有`count[key]+=tmp[key]`.

此处有一个非常重要的优化技巧。我们在合并tmp与count的时候，遍历的是tmp里面的key。但是如果我们发现count.size()比tmp小的时候，可以先swap(tmp,count)，以减少需要遍历的key的数目。
