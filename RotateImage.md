You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/156603629-cced5f9e-b0b3-4afa-b5b6-42a852abfab3.png)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
```

Approach:- either can move each element or can use clever matrix operation(should have learned linear algebra ;) )

So the approach i will explain is of transpose + reversal. Transpose is a method in which row and columns are inter-switched

```
public void rotate(int[][] matrix) {
   int n = matrix[0].length;
   for(int i=0;i<matrix.length;i++){
      for(int j=i+1;j<matrix[0].length;j++){
          int tmp = matrix[j][i];
          matrix[j][i] = matrix[i][j];
          matrix[i][j] = tmp;
      }  
   }
   
   for(int i=0;i<matrix.length;i++){
      for(int j=0;j<(n/2);j++){
          int tmp = matrix[i][j];
          matrix[i][j] = matrix[i][n-j-1];
          matrix[i][n-j-1] = tmp;
      }  
   }
}
```

Time complexity - O(N) where N is all elements
Space complexity - O(1)


