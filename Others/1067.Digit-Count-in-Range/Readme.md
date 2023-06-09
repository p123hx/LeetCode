### 1067.Digit-Count-in-Range

如果digit不是0的话，代码完全类似于`233. Number of Digit One`，用一个helper函数计算[1,n]的数字d的出现次数，然后返回`helper(high)-helper(low-1)`.

233的基本思想就是逐个位数的考虑，计算出现digit的次数。比如说num=2452，digit=4

考虑个位时，就是计算出现XXX1的次数。如果XXX是从000到234，显然都是必然可行的。如果XXX是235的话，因为个位数是2小于4，所以不可以。因此count+=235*1;

考虑十位时，就是计算出现XX1Y的次数。如果XX是从00到22，显然，都是必然可行的，此时固定十位数字是4的话，Y位可以是任意数，因此count+=23\*10. 接下来考虑XX如果是23的话，因为十位是5大于4，所以Y可以是任意数。所以补上 count+=10.

考虑百位时，就是计算出现X1YY的次数。如果X是从0到1，显然，都是必然可行的，此时固定百位数字是4的话，YY位可以是任意数，因此count+=2\*100. 接下来考虑X如果是2的话，因为百位是4等于digit，所以YY可以是从00-52的任意数。所以补上 count+=53.

考虑千位时，直接考虑4YYY的次数。因为千位数是2小于4，所以千位数上是digit的次数是0.

总结一下，对于从低到高的第i位（最低为第一位）出现d的次数，就是计算所有XXdYY的个数。考虑两点：
1. d前面的数字从00取至(XX-1)时，YY都可以取任何数字(00-99)，所以出现d的次数是 ```XX*pow(10,i-1)```
2. d前面的数字固定为XX时，我们需要判断第i位是否比d大：如果是的话，那么第i位取d时，YY可以是任何数(00-99)，所以增加pow(10,i-1). 如果第i位等于d，那么我们增加的个数就是YY。如果第i位小于d，那么显然第i位上不可能再取到d，不增加。

如果digit是0的话，唯一的区别在于第一条。d前面的数字只能从1取至(XX-1)，这样的话YY可以取任何数字(00-99)，所以出现d的次数是 ```(XX-1)*pow(10,i-1)```.至于XX为什么不能取00呢？因为XX如果取00，接下来的第i位也是0，那么这些都是leading zeros，计算第i位的0出现的次数是没有意义的。


[Leetcode Link](https://leetcode.com/problems/digit-count-in-range)
