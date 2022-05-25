### The question

Given a rod of length n inches and an array of prices that includes prices of all pieces of size smaller than n. Determine the maximum value obtainable by cutting up the rod and selling the pieces. For example, if the length of the rod is 8 and the values of different pieces are given as the following, then the maximum obtainable value is 22 (by cutting in two pieces of lengths 2 and 6) 
```
length   | 1   2   3   4   5   6   7   8  
--------------------------------------------
price    | 1   5   8   9  10  17  17  20
```

And if the prices are as following, then the maximum obtainable value is 24 (by cutting in eight pieces of length 1) 

```
length   | 1   2   3   4   5   6   7   8  
--------------------------------------------
price    | 3   5   8   9  10  17  17  20
```

Approach:-

![Screenshot 2022-05-25 at 8 57 46 PM](https://user-images.githubusercontent.com/18497513/170299636-50b5d431-c3e8-46b3-9a2f-212990696343.png)
 
Lets code:-

```
public int solution(int[] prices){
  int n = prices.length;
  int np[] = new int[n+1];
  
  for(int i=0;i<n; i++){
      np[i+1] = prices[i];
  }
  
  int dp[] = new int[np.length];
  dp[0] = 0;
  dp[1] = np[1];
  for(int i=2; i<np.length+1; i++){
     dp[i] = np[i];
     int l = 1;
     int r = i-1;
     
     while(li<=ri){
        if(dp[l]+dp[r]>dp[i]){
              dp[i] = dp[l]+dp[r];
        }
        
        li++;
        ri--;
     }   
  }
  
  return dp[dp.length-1];
}
```

Time complexity - O(n^2)
Space complexity - O(n) 
