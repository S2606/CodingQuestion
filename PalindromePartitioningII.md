### The question

Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

Example 1:

```
Input: s = "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
```

Approach:-

![Screenshot 2022-05-31 at 9 52 21 PM](https://user-images.githubusercontent.com/18497513/171224106-1b66482a-85c4-4653-abc5-d943bc77a75b.png)

Lets code:-

```
public int minCut(String s) {
        int n = s.length();
        boolean dpPalindrome[][] = new boolean[n][n];
        int dp[][] = new int[n][n];
        
        for(int g=0; g<n; g++){
            for(int i=0, j=g; j<n; i++, j++){
                if(g==0){
                    dpPalindrome[i][j] = true;  
                } else if(g==1){
                    if(s.charAt(i)==s.charAt(j)){
                        dpPalindrome[i][j] = true;
                    } else {
                        dpPalindrome[i][j] = false;
                    }
                } else {
                    if(s.charAt(i)==s.charAt(j) && dpPalindrome[i+1][j-1]==true){
                        dpPalindrome[i][j] = true;
                    } else {
                        dpPalindrome[i][j] = false;
                    }
                }
            }
        }
        
        for(int g=0; g<n; g++){
            for(int i=0, j=g; j<n; i++, j++){
                if(g==0){
                    dp[i][j] = 0;
                } else if(g==1) {
                    if(s.charAt(i)==s.charAt(j)){
                        dp[i][j] = 0;
                    } else {
                        dp[i][j] = 1;
                    }
                } else {
                    if(dpPalindrome[i][j]){
                        dp[i][j] = 0;
                    } else {
                        int min = Integer.MAX_VALUE;
                    
                        for(int k=i; k<j; k++){
                            int left = dp[i][k];
                            int right = dp[k+1][j];
                            
                            int sum = left+right+1;
                            min = Math.min(min, sum);
                        }   
                        
                        dp[i][j] = min;
                    }
                }
            }
        }
        
        return dp[0][s.length()-1];
    }
```

Time complexity - O(n^3) - has three for loop, the last for loop can have worst n entries hence O(n^3)
Space complexity - O(n^2) - 2d-Arrays

Can we further optimize this??
- How about using only 1D Array for finding minimum cuts, given the previous 2D-Array which store the falsability of palindromin substring is there. How this will work??

![Screenshot 2022-06-02 at 11 46 21 AM](https://user-images.githubusercontent.com/18497513/171565240-b66989e4-5c2f-4f67-8a0f-a13b418f1624.png)

Lets code:-

```
public int minCut(String s) {
        int n = s.length();
        boolean dpPalindrome[][] = new boolean[n][n];
        int dp[] = new int[n];
        
        for(int g=0; g<n; g++){
            for(int i=0, j=g; j<n; i++, j++){
                if(g==0){
                    dpPalindrome[i][j] = true;  
                } else if(g==1){
                    if(s.charAt(i)==s.charAt(j)){
                        dpPalindrome[i][j] = true;
                    } else {
                        dpPalindrome[i][j] = false;
                    }
                } else {
                    if(s.charAt(i)==s.charAt(j) && dpPalindrome[i+1][j-1]==true){
                        dpPalindrome[i][j] = true;
                    } else {
                        dpPalindrome[i][j] = false;
                    }
                }
            }
        }
        
       dp[0] = 0;
       
        for(int j=1; j<n; j++){
            if(dpPalindrome[0][j]){
                dp[j] = 0;
            } else {
                int min = Integer.MAX_VALUE;
                
                for(int i=j; i>=1; i--){
                    if(dpPalindrome[i][j]){
                        min = Math.min(min, dp[i-1]);
                    }
                }
                
                dp[j] = min+1;
            }
        }
        
        return dp[n-1];
    }
```

Time complexity - O(n^2) - has two for loop, the last for loop can have worst n entries hence O(n^2)
Space complexity - O(n^2) - 2d-Arrays

