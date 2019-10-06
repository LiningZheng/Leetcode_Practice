### 1 
use a 1-one-bit mask whose one-bit position moves from right to left.
accompanied with a loop to calculate the result of each bit, considering the carries from previous bit position.

### 2 more concise.
```java
class Solution {
    public int getSum(int a, int b) {
        return (b == 0) ? a : getSum(a^b, (a&b) << 1);
    }
}
```
from: 

https://leetcode.com/problems/sum-of-two-integers/discuss/84278/A-summary%3A-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently


do the carries of all the bits at the same time. 
Note that it applies to negatives too, because the negatives are stored as "complement code" in the binary form. 
