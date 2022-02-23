There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return true if you can finish all courses. Otherwise, return false.

Example 1:
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

Approach:- Classic case of topological sort, if sorted oder == no.of courses then true else false. Note here we take each course as vertices of a graph and 
relation between two courses as unweighted edges of graph

```
static LinkedList<Integer> adjencyList[];

public ArrayList<Integer> returnTopologicalSort(int numCourses){
  ArrayList<Integer> result = new ArrayList();
  Stack<Integer> stk = new Stack<>();
  Boolean[] visited = new Boolean[numCourses];
  for(int i=0;i<numCourses;i++){
    visited[i] = false;
  }
  
  for(int i=0;i<numCourses;i++){
     if(visited[i]==false){
        topologicalSort(i, stk, visited, numCourses);
     }
  }
  
  while(!stk.isEmpty()){
    list.add(stk.pop());
  }
  
  return list;
}

public void topologicalSort(int i, Stack<Integer> stk, Boolean[] visited, int numCourses){
    visited[i] = false;
    List<Integer> adjList = adjencyList[i];
    for(int ele: adjList){
        if(visited[ele]==false){
            topologicalSort(ele, stk, visited, numCourses);
        }
        stk.add(ele);
    }
}

public boolean canFinish(int numCourses, int[][] prerequisites) {
    int noOfEdges = prerequisites.length;
    adjencyList = new LinkedList[numCourses];
    for(int i=0; i<numCourses; i++){
      adjencyList[i] = new LinkedList<>();
    }
    for(int i=0;i<noOfEdges;i++){
      int[] edge = prerequisites[i];
      adjencyList[edge[0]].add(edge[1]);
    }
    
    ArrayList<Integer> arryList = returnTopologicalSort(numCourses);
    
    if(arryList.size()==numCourses){
        Boolean[] visited = new Boolean[numCourses];
        for(int ele: arryList){
           visited[ele] = true;
           List<Integer> adjList = adjencyList[ele];
           for(int j: adjList){
              if(visited[j]) return false;
           }
        }
        return true;
    }
    
    reutrn false;
}
```
Time complexity - O(E+V^2) Why? E is for generating the adjency list, one V is for checking topoligical sort for all vertices, other is traversing all elements inside that sort.

Space complexity - O(E+V)

Okay, this and all is coll but can we further optimize it?

The hypothesis that can be considered is that from the first node in the chain, if no cycle was detected, then all its desendants will also not have a cycle eight?

So i guess this redundant step can be removed

```
static LinkedList<Integer> adjencyList[];

public boolean canFinish(int numCourses, int[][] prerequisites) {
   int noOfEdges = prerequisites.length;
    adjencyList = new LinkedList[numCourses];
    for(int i=0; i<numCourses; i++){
      adjencyList[i] = new LinkedList<>();
    }
    for(int i=0;i<noOfEdges;i++){
      int[] edge = prerequisites[i];
      adjencyList[edge[0]].add(edge[1]);
    }
    
    boolean[] checked = new boolean[numCourses];
    boolean[] path = new boolean[numCourses];
    
    for(int i=0; i<numCourses; i++){
      if(this.isCycle(i, checked, path)){
        return false;
      }
    }
}

public boolean isCycle(int currCourse, boolean[] checked, boolean[] path) {
  if(checked[currCourse]==true)
    return false;
    
  if(path[currCourse]==true)
    return true;
    
  if(adjencyList[currCourse].size()==0)
    return false;
    
  path[currCourse] = true;
  
  boolean ret = false;
  
  List<Integer> adjList = adjencyList[currCourse];
  for(int ele: adjList){
      ret = this.isCycle(ele, checked, path);
      if(ret)
        return true;
  }
  
  path[currCourse] = false;
  
  checked[currCourse] = true;
  return ret;
}
```
Time complexity - O(E+V) Why? E is for generating the adjency list,only one V is required for checking topoligical sort for all vertices

Space complexity - O(E+V)

