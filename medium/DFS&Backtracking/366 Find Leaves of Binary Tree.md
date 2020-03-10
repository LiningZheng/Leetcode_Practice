### 1
```java
public List<List<Integer>> findLeaves(TreeNode root) {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    
    DFS(root, res);
    
    return res;
}

private int DFS(TreeNode root, List<List<Integer>> res) {
    if (root == null) return 0;
    
    int leftHeight = DFS(root.left, res);
    int rightHeight = DFS(root.right, res);
    int height = Math.max(leftHeight, rightHeight) + 1;
    
    if (res.size() < height) {
        List<Integer> newList = new LinkedList<Integer>();
        newList.add(root.val);
        res.add(newList);
    } else {
        // careful. It's height - 1 !
        res.get(height - 1).add(root.val);
    }
    
    return height;
}
```

The position where the node should be put depends on its maximum height (max distance from the node to a leaf).

A more intuitive idea would be to first use a seperate recursion to get the max height of the root so that we can figure out the size of the result array.

However, this is not necessary. We can just increase the array size in the recursion for computing the max height because the bottom of the tree should be put at the head of the array.
