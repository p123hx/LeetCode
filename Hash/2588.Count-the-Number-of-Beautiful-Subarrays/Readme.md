### 2588.Count-the-Number-of-Beautiful-Subarrays

#### 解法1：
本题翻译一下，其实就是找符合条件的subarray的数目，使得subarray里面的元素，在每个二进制bit上出现1的次数都是偶数。这样我们每次操作可以消灭一对在某个bit上的1，操作若干次之后会把所有bit上的1都消灭。

对于subarray的题目，考虑前缀是一个比较自然的想法。假设某个subarray [a:b]是符合要求的，那么意味着前缀[0:b]在每个bit上出现1的次数的奇偶性，必然与前缀[0:a-1]的奇偶性相同。这样两者一减，必然就有[a:b]的元素在每个二进制bit上出现1的次数是偶数。

所以我们遍历b的位置，将[0:b]里每个bit上出现1的次数的奇偶性编码为一个32位的二进制整数state，我们则只需要检查在之前出现的前缀里，这样的编码state出现了几次，就意味着有多少前缀位置可以和b匹配构成一个subarray。

特别注意，初始情况下对应编码0，要有初始值`Map[0] = 1`，否则会遗漏以下标0为左端点的subarray。

#### 解法2：
其实我们可以用subarray里面元素的异或和，来表示每个bit上出现1的的次数的奇偶性。与解法1相比可以省略对每个bit的循环操作。
