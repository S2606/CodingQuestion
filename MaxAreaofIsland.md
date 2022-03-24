### The question

You are given an m x n binary matrix grid. An island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.
The area of an island is the number of cells with a value 1 in the island.

Return the maximum area of an island in grid. If there is no island, return 0.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/159848895-c53fb750-3923-4d9a-a0d6-230d8e7c24e1.png)

```
Input: grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output: 6
Explanation: The answer is not 11, because the island must be connected 4-directionally.
```

Approach:-

![Screenshot 2022-03-24 at 11 15 10 AM](https://user-images.githubusercontent.com/18497513/159850494-6054dbbc-da65-4365-b3a8-a7777b58ee53.png)

Lets code

```
int[][] grid;
boolean[][] seen;

public int area(int r, int c){
  if(r > grid.length || r < 0 || c > grid[0].length || c < 0 || boolean[r][c]){
      reutrn 0;
  }
  
  seen[r][c] = true;
  return 1 + area(r, c-1) + area(r, c+1) + area(r-1, c) + area(r+1, c);
}

public int maxAreaOfIsland(int[][] grid) {
  this.grid = grid;
  seen = new boolean[grid.length][grid[0].length];
  
  int area = 0;
  for(int i=0;i<grid.length;i++){
      for(int j=0;j<grid[0].length;j++){
        area = Math.max(area, area(i, j);
      }
  }
  
  return area;
}
```

- Time complexity - O(r*c) where r is no. of rows and c is no. of columns
- Space complexity - O(r*c)
