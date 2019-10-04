### Solution 1
check the relation with the previous

```java
class Solution {
    public String countAndSay(int n) {
        String res = "1";
        for (int i = 0; i < n - 1; i++) {
            res = nextStr(res);
        }
        return res;
    }
    
    private String nextStr(String str) {
        int curPos = 1;
        StringBuilder sb = new StringBuilder();
        int counter = 1;
        
        while (curPos < str.length()) {
            if (str.charAt(curPos) == str.charAt(curPos - 1)) {
                counter += 1;
            }
            else {
                sb.append(counter);
                sb.append(str.charAt(curPos - 1));
                counter = 1;
            }
            curPos += 1;
        }
        sb.append(counter);
        sb.append(str.charAt(curPos - 1));
        return sb.toString();
    }
}
```

有点小卡

the problem lies in the iteration model..

after the middle case, think about the initial case. also keep in mind the meaning of each variable at the start of the iteration


### Solution 2
check the relation with the next
```java
class Solution {
    public String countAndSay(int n) {
        String res = "1";
        for (int i = 0; i < n-1; i++) {
            res = nextStr(res);
        }
        return res;
    }
    
    private String nextStr(String str) {
        int curPos = 0;
        int counter = 0;
        StringBuilder sb = new StringBuilder();
        while (curPos < str.length()) {
            if (curPos == str.length() - 1) {
                sb.append(counter + 1);
                sb.append(str.charAt(curPos));
                break;
            }
            if (str.charAt(curPos + 1) == str.charAt(curPos)) {
                counter += 1;
            } else {
                sb.append(counter + 1);
                sb.append(str.charAt(curPos));
                counter = 0;
            }
            curPos += 1;
        }
        return sb.toString();
    }
}
```
