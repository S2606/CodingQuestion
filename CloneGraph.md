## The question

Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

Each node in the graph contains a value (int) and a list (List[Node]) of its neighbors.

class Node {
    public int val;
    public List<Node> neighbors;
}

Example:-

Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
Explanation: There are 4 nodes in the graph.
1st node (val = 1)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
2nd node (val = 2)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
3rd node (val = 3)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
4th node (val = 4)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).

Intuition:- Basically just have like a side-car wherein node and clonedNode kinda move side-by-side. Can either go DFS or BFS. In order to implement side-car approach use a simple hashMap.

Code:-
```
private HashMap<Node, Node> visited = new HashMap();
public Node cloneGraph(Node node) {
    if(node==null){
        return node;
    }

    if(visited.containsKey(node)){
       return visited.get(node);
    }

    Node clonedNode = new Node(node.val, new ArrayList());
    visited.put(node, clonedNode);

    for(Node neighbour: node.neighbors){
        clonedNode.neighbors.add(cloneGraph(neighbour));
    }

    return clonedNode;
}
```

Time complexity - O(N+M) where N is no. of nodes and M is no. of edges
Space complexity - O(N)
