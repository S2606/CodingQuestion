## The question

You are given an integer n denoting the number of nodes of a weighted directed graph. The nodes are numbered from 0 to n - 1.

You are also given a 2D integer array edges where edges[i] = [fromi, toi, weighti] denotes that there exists a directed edge from fromi to toi with weight weighti.

Lastly, you are given three distinct integers src1, src2, and dest denoting three distinct nodes of the graph.

Return the minimum weight of a subgraph of the graph such that it is possible to reach dest from both src1 and src2 via a set of edges of this subgraph. In case such a subgraph does not exist, return -1.

A subgraph is a graph whose vertices and edges are subsets of the original graph. The weight of a subgraph is the sum of weights of its constituent edges.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/158289972-b14f9a14-ee79-4798-b53b-bb193749d9cb.png)

```
Input: n = 6, edges = [[0,2,2],[0,5,6],[1,0,3],[1,4,5],[2,1,1],[2,3,3],[2,3,4],[3,4,2],[4,5,1]], src1 = 0, src2 = 1, dest = 5
Output: 9
Explanation:
The above figure represents the input graph.
The blue edges represent one of the subgraphs that yield the optimal answer.
Note that the subgraph [[1,0,3],[0,5,6]] also yields the optimal answer. It is not possible to get a subgraph with less weight satisfying all the constraints.
```

Approach:- Do you know what Dijkstra is?? Bhai ko kaam mat samajh. Djkstra's algorithm helps in finding shortest path from a point i in a graph. 
Time complexity - O(V+E)logV). In this algo, the only difference with bfs traversal is that we use a PriorityQueue for sorting the weight the choose the smallest one,
thereby being a Greedy approach to solve the problem.

In order to solve this, we know that there will be a common point i through which both sources shall go through and reach the destination. so lets break the problem into three parts
- find shortest path from src1 till i
- find shortest path from src2 till i
- find shortest path from i till dest

![Screenshot 2022-03-15 at 7 27 14 AM](https://user-images.githubusercontent.com/18497513/158290705-e2779093-7363-4658-8376-a9da81b230f5.png)

Also for solving i till dest, we need to create sort of reverse adjacent list which would say that point x was reached through point y with weight w.

lets code!

```
    ArrayList<int[]> [] al, ral;
    public long minimumWeight(int n, int[][] edges, int src1, int src2, int dest) {
        buildGraph(n, edges);
        
        long [] src1To = new long[n], src2To = new long[n], toDest = new long[n];
        Arrays.fill(src1To, -1);
        Arrays.fill(src2To, -1);
        Arrays.fill(toDest, -1);
        
        djkstra(src1, src1To, al);
        djkstra(src2, src2To, al);
        djkstra(dest, toDest, ral);
        
        long res = -1;
        for(int i=0;i<n;i++){
            long src1Dist = src1To[i]; 
            long src2Dist = src2To[i];
            long destDist = toDest[i];
            
            if(src1Dist > -1 && src2Dist > -1 && destDist > -1){
                long dist = src1Dist + src2Dist + destDist;
                if(res==-1 || res > dist){
                    res = dist;
                }
            }
            
        }
        
        return res;
    }
    
    public void buildGraph(int n, int[][] edges){
        al = new ArrayList[n];
        ral = new ArrayList[n];
        
        for(int i=0;i<n;i++){
            al[i] = new ArrayList();
            ral[i] = new ArrayList();
        }
        
        for(int i=0;i<edges.length;i++){
            int src = edges[i][0];
            int dest = edges[i][1];
            int weight = edges[i][2];
            al[src].add(new int[]{dest, weight});
            ral[dest].add(new int[]{src, weight});
        }
    }
    
    public void djkstra(int point, long [] dist, ArrayList<int[]> [] al){
        PriorityQueue<long[]> queue = new PriorityQueue<>((a, b) -> Long.compare(a[1], b[1]));
        queue.add(new long[]{point, 0});
        
        while(!queue.isEmpty()){
            long[] res = queue.poll();
            int dest = (int) res[0];
            long weight = res[1];
            if(dist[dest] != -1 && dist[dest] <= weight){
                continue;
            }
            dist[dest] = weight;
            for(int[] nextPnt: al[dest]){
                queue.add(new long[]{nextPnt[0], weight+nextPnt[1]});
            }
        }
    }
}
```

Time Complexity - O(3(V+E)logV)

Space Complexity - O(3V + VE)
