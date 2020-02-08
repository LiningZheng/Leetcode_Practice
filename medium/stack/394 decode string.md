### 1
```Java
class Solution {
    public String decodeString(String s) {
        String res = "";
        Stack<String> resStack = new Stack<>();
        resStack.push(res);
        Stack<Integer> countStack = new Stack<>();
        
        int index = 0;
        while(index < s.length()){
            char curChar = s.charAt(index);
            if(Character.isDigit(curChar)){
                //System.out.println("found digit: "+ curChar);
                int count = 0;
                while(Character.isDigit(s.charAt(index)) && index < s.length()){
                    count = count * 10 + (s.charAt(index) - '0');
                    index++;
                }
                countStack.push(count);
                continue; // to skip index++
            } else if(curChar == '['){
                resStack.push(res);
                res = "";

            } else if(curChar == ']'){
                StringBuilder sb = new StringBuilder(resStack.pop());
                int count = countStack.pop();
                for(int i = 0; i < count; i++){
                    sb.append(res);
                }
                res = sb.toString();
            } else {
                res += curChar;
            }
            index ++;
        }
        return res;
    }
    
}
```

* understand stack. each push means you are entering a deeper level..
