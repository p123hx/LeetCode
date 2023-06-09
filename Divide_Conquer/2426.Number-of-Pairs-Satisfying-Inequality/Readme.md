### 2426.Number-of-Pairs-Satisfying-Inequality

稍微转化一下题意，令`arr[i] = nums1[i]-nums2[i]`，本题即是求在arr里的index pair {i,j}，满足`arr[i] <= arr[j]+diff`.

显然，本题很像求数组里的“正序对”数目，自然解法和求数组“逆序对”数目也一模一样，就是经典的分治法。和315,327,493,1649属于同一类型。

分治法的递归思想：将区间分为前后两部分，各自递归处理，且保持有序。这样，对于后半部分的每一个arr[j]，我们很容易知道在前半部分有多少arr[i]满足`arr[i] <= arr[j]+diff`（用一个指针滑动即可）。然后，将区间的前后两部分归并排序使整个区间继续保持有序，返回。

仔细体会，为什么这种方法可以对任意的arr[j]可以穷举到每一个符合的arr[i]？核心在于任何一个在j之前的i，必然会在某个区间内满足：i在前半区间，j在后半区间。
