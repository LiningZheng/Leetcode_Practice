### 1 Naive Solution
which didn't pass xD

O(n^2) time, memory
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int dp[][] = new int[n][n];
        int maxNum = Integer.MIN_VALUE;
        
        for (int i = 0; i < n; i++) {
            dp[i][i] = nums[i];
            maxNum = Math.max(maxNum, dp[i][i]);
            for (int j = i+1; j < n; j++) {
                dp[i][j] = dp[i][j-1] + nums[j];
                maxNum = Math.max(maxNum, dp[i][j]);
            }
        }
        return maxNum;
        
    }
}
```

### 2 A smarter way of DP 
the max sequence that ends here is the larger between 
1) (max sequence ends with previous num) + curNum

2) curNum (abandoning the previous sequence)

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxEndingHere = nums[0];
        int maxSofar = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(maxEndingHere + nums[i], nums[i]);
            maxSofar = Math.max(maxSofar, maxEndingHere);
        }
        return maxSofar;
    }
}
```
