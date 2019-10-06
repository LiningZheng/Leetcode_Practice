### 1
```java
class Solution {
    public String toHex(int num) {
        int i = 0;
        StringBuilder sb = new StringBuilder();
        int mask = 0x0000000F;
        do {
            int partRes = num & mask;
            char c = (partRes > 9) ? (char)('a' + partRes - 10) : (char)('0' + partRes);
            sb.append(c);
            num >>>= 4;
            i += 1;
        } while (i < 8 && num != 0); // use num != 0 to break the loop to avoid excessive 0 in the front 
        sb = sb.reverse();
        return sb.toString();
    }
}
```

