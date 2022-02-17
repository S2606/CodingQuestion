## The question

Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

    For example, "ace" is a subsequence of "abcde".

A common subsequence of two strings is a subsequence that is common to both strings.

This seems to be classic case of DP. Why?

```
1) Identify if it is a DP problem
  1.1) Does it statisfy Optimal Substructure Property?
    - Let input be A[0..m-1] and B[0..n-1], in order to find LCS of A, B 
      if A[m-1] == B[n-1]  the formula is L(A[0..m-1], B[0..n-1]) = 1 +  L(A[0..m-2], B[0..n-2])
      else L(A[0..m-1], B[0..n-1]) = MAX(L(A[0..m-1], B[0..n-2]), L(A[0..m-2], B[0..n-1]))
  1.2) Does it statisfy Overlapping Substructure Property?
    - Can a recursion related solution be made from this? Yes
      ```
      int rec(char[] A, char[] B, int m, int n){
          if(m==0 || n==0){
             return 0;
          } else if(A[m-1]==B[n-1]){
             return 1 + rec(A, B, m-1, n-1);
          } else {
             return Math.max(rec(A, B, m, n-1), rec(A, B, m-1, n));
          }
      }
      ```
2) Decide a state expression with least parameters
   dp[i][j] this means longest common subsequence between A[i] and B[j]
   
3) Formulate state relationship
   if A[m-1] == B[n-1]  the formula is dp[i][j] = 1 +  dp[i-1][j-1]
   else dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1])
   
4) Memonize
   Store it in 2d Array
```

I guess code is the only thing that is left

```
int lcs(char[] a, char[] b){
    int m = a.length;
    int n = b.length;
    int dp[][] = new int[m][n];
    
    for(int i=0;i<m;i++){
        for(int j=0;j<n;j++){
            if(i==0 || j==0){
                dp[i][j] = 0;
            } else if(a[i]==b[j]){
               dp[i][j] = 1 - dp[i-1][j-1];
            } else {
               dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    
    return dp[i-1][j-1];
}
```
