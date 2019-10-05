### 1
1) calculate n! 

2) result / 10 repeatedly

### 2 
calculate n! 
during the process, whenever see a trailing 0: count += 1; result = result / 10

### 3 a subtle way.

```java
class Solution {
    public int trailingZeroes(int n) {
        if (n == 0) return 0;
        
        return n / 5 + trailingZeroes (n / 5);
    }
}
```

trailing zeros come from factors 2 and 5. 
the # of 2 is obviously more than # of 5 

equivalent====> count how many 5 factors are there from n!


observation: 

every 5 counts, there's a 5 factor. e.g., 1,2,3,4,5!6,7,8,9,10!

based on that, every 25 counts, there's a bonus 5 factor  e.g., 1~5,6~10,10~15,16~20,21~25!

.... think inductively

we can imagine unwrapping an onion xD.

e.g., n = 25. after the first unwrapping of those with a 5 factor, the sequence becomes 1,2,3,4,5.. do it recursively :D

It's a math problem >.<
