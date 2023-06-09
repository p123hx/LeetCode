### 2555.Maximize-Win-From-Two-Segments

为了尽量大地增加收益，我们肯定不会让这两段区间重叠，即会让两段区间各自占满k的长度；除非总长度小于2k，那样的话，我们就取全部的点即可。

接下来我们考虑，如何取一段长度为k的区间，使得区间内包含的点的数目最多。这个也很容易，只要确定了左端点i，那么单向移动右端点j即可，当恰好`p[j]-p[i]>k`时，说明`j-i`就是以i为左端点的、长度为k的区间的最大元素数目，我们记做left[i]。同理，我们也可以计算以j为右端点的、长度为k的区间的最大元素数目right[j]。

那么回到两个区间的问题。因为两段区间不重合，所以我们只要找一个分界点k，在k左边找一个最大数目区间（注意其右端点不一定就是在k），在k右边找一个最大数目区间（注意其左端点也不一定就是k），两者之和就是以k为分界点所能得到的两个区间。注意到，前者是right[j]的前缀Max，后者是left[i]的后缀Max。
