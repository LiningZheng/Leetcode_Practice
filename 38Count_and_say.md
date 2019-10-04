
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

