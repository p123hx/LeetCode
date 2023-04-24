### 11. Container With Most Water 
#### Greedy; Two Pointer  
Obviously this is O(n)
And clearly we start with 2 pointers from both sides for "water container" kinda question.
KEY is: do we move left or right or both pointers? We move the lower pointer: 
(GREEDY) What if: next high pointer h2 is higher than current high pointer h1? 
=> since the volumn is determined by lower pointer, it's still getting lower.
```cpp
if (height[left]>=height[right])
   right--;
else
   left++;
```


[Leetcode Link](https://leetcode.com/problems/container-with-most-water)
