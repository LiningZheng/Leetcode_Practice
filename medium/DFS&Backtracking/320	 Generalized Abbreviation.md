description

Given word = "word", return the following list (order does not matter):
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]

so the rules are:
replace a character with a number or not.
if there are more than 2 numbers together, add them up. 


### 1 DFS 

```java
public List<String> generateAbbreviations(String word) {
   List<String> res = new LinkedList<String>();
   DFS(word, new StringBuilder(), 0, 0, res);
   return res;
}

private void DFS(String word, StringBuilder sb, 
       int curPos, int prevCount, List<String> res) {
   if (curPos >= word.length()) {
       res.add(sb.toString());
       return;
   }

   StringBuilder sbClone = new StringBuilder(sb); // clone always chooses to replace it with a number
   if (prevCount > 0) {
       sbClone.deleteCharAt(sbClone.length() - 1);
       sbClone.append(prevCount + 1);
   }  else {
       sbClone.append(1);
   }
   DFS(word, sbClone, curPos + 1, prevCount + 1, res);

   sb.append(word.charAt(curPos));
   DFS(word, sb, curPos + 1, 0, res);
}
```
