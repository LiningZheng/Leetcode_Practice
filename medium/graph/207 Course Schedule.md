### 1 BFS
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses <= 0 || prerequisites.length <= 0) return true;
        
        int numUnfinished = numCourses;
        int[] remainingCourse = new int[numCourses]; // A.K.A, array keeping track of the indegree 
        Arrays.fill(remainingCourse, 0);
        
        //a queue for newly finished courses.
        Queue<Integer> queue = new LinkedList<Integer>();
        
        List<List<Integer>> graph = new ArrayList<>(numCourses);
        for (int i = 0; i < numCourses; i++) {
            graph.add(new LinkedList<Integer>());
        }
        
        for (int[] pair : prerequisites) {
            graph.get(pair[1]).add(pair[0]);
            remainingCourse[pair[0]] += 1;
        }
        
        for(int i = 0; i < numCourses; i++) {
            if (remainingCourse[i] == 0) 
                queue.offer(i);
        }
        
        while (!queue.isEmpty()) {
            int finishedCourse = queue.poll();
            numUnfinished -= 1;
            
            for (int course : graph.get(finishedCourse)) {
                remainingCourse[course] -= 1;
                if (remainingCourse[course] == 0) 
                    queue.offer(course);
            }
        }
        
        return numUnfinished == 0;
    }
}
```

If the labels of the nodes are not from 0 to n-1, a hash map can be used.

### 2 DFS

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses <= 0 || prerequisites.length <= 0) return true;
        
        List<List<Integer>> graph = new ArrayList<>(numCourses);
        for (int i = 0; i < numCourses; i++) {
            graph.add(new LinkedList<Integer>());
        }
        // build the graph
        for (int[] pair : prerequisites) {
            graph.get(pair[0]).add(pair[1]);
        }
        
        boolean[] checked = new boolean[numCourses];
        boolean[] visited = new boolean[numCourses];
        Arrays.fill(checked, false);
        Arrays.fill(visited, false);
        
        for (int i = 0; i < numCourses; i++) {
            if (findCycle(graph, i, checked, visited)) return false;
        }
        
        return true;
    }
    
    private boolean findCycle(List<List<Integer>> graph, int curPos,
                             boolean[] checked, boolean[] visited) {
                             
        // this order of checking visited[curPos] and checked[curPos] cannot be reversed.
        if (visited[curPos]) return true;
        if (checked[curPos]) return false;
        
        checked[curPos] = visited[curPos] = true;
        for (int nextCourse : graph.get(curPos)) {
            if(findCycle(graph, nextCourse, checked, visited))
                return true;
        }
        visited[curPos] = false;
        return false;
    }
}
```

to check if there's a cycle in the graph. 

=====================
### What about detecting cycles in an undirected graph?
### 1 
it could be the same as the DFS solution as above, using boolean array to keep track of the visited ones

### 2
using one boolean array for tracking, inputing parent node for the recursive function.

```java
class Solution {
    boolean main(....) {
        List<List<Integer>> graph = new ArrayList<>(numCourses);
        //building the graph and so on...........
                boolean[] visited = new boolean[numCourses];
        Arrays.fill(visited, false);
        
        for (int i = 0; i < numCourses; i++) {
            if (visited[i]) continue;
            if (findCycle(graph, -1, i, visited)) return false;
        }
        
        return true;
    }
    
    private boolean findCycle(
        List<List<Integer>> graph, 
        int parentNode, 
        int curNode, 
        boolean[] visited) {
        
        visited[curNode] = true;
        
        for (int neighbor : graph.get(curNode)) {
            if (neighbor != parentNode && visited[neighbor]) 
                return true;
            if (findCycle(graph, curNode, neighbor, visited))
                return true;
        }
        
        return false;
    }
}
```
