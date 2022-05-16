### The question

You have a convex n-sided polygon where each vertex has an integer value. You are given an integer array values where values[i] is the value of the ith vertex (i.e., clockwise order).

You will triangulate the polygon into n - 2 triangles. For each triangle, the value of that triangle is the product of the values of its vertices, and the total score of the triangulation is the sum of these values over all n - 2 triangles in the triangulation.

Return the smallest possible total score that you can achieve with some triangulation of the polygon.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/168467739-52d6e5ca-af2d-488b-8202-8b2cbaa2a0e9.png)

Input: values = [1,2,3]
Output: 6
Explanation: The polygon is already triangulated, and the score of the only triangle is 6.

Approach:- 

![Screenshot 2022-05-16 at 10 23 02 PM](https://user-images.githubusercontent.com/18497513/168643959-e1b4bc2c-94b6-44ea-b27e-d04dfd108231.png)

Lets code:-

```
public int minScoreTriangulation(int[] values) {
    int dp[][] = new int[values.length][values.length];

    for(int g = 0; g < dp.length; g++){
        for(int i=0, j=g; j<dp[0].length; i++, j++){
            if(g==0){
                dp[i][j] = 0;
            } else if(g==1){
                dp[i][j] = 0;
            } else if(g==2){
                dp[i][j] = values[i] * values[i+1] * values[i+2];
            } else {
                int min = Integer.MAX_VALUE;

                for(int k=i+1; k<=j-1; k++){
                    int pleft = dp[i][k];
                    int pright = dp[k][j];

                    int tri = values[i] * values[j] * values[k];

                    int tmin = pleft + tri + pright;

                    if(tmin < min){
                        min = tmin;
                    }
                }

                dp[i][j] = min;
            }
        }
    }

    return dp[0][values.length-1];
}
```

Time complexity - O(n^2)
Space complexity - O(n^2)
