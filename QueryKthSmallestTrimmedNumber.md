## Question

You are given a 0-indexed array of strings nums, where each string is of equal length and consists of only digits.

You are also given a 0-indexed 2D integer array queries where queries[i] = [ki, trimi]. For each queries[i], you need to:

    Trim each number in nums to its rightmost trimi digits.
    Determine the index of the kith smallest trimmed number in nums. If two trimmed numbers are equal, the number with the lower index is considered to be smaller.
    Reset each number in nums to its original length.

Return an array answer of the same length as queries, where answer[i] is the answer to the ith query.

Note:

    To trim to the rightmost x digits means to keep removing the leftmost digit, until only x digits remain.
    Strings in nums may contain leading zeros.

Example
```
Input: nums = ["102","473","251","814"], queries = [[1,1],[2,3],[4,2],[1,2]]
Output: [2,2,1,0]
Explanation:
1. After trimming to the last digit, nums = ["2","3","1","4"]. The smallest number is 1 at index 2.
2. Trimmed to the last 3 digits, nums is unchanged. The 2nd smallest number is 251 at index 2.
3. Trimmed to the last 2 digits, nums = ["02","73","51","14"]. The 4th smallest number is 73.
4. Trimmed to the last 2 digits, the smallest number is 2 at index 0.
   Note that the trimmed number "02" is evaluated as 2.
```

Approach:-

![Screenshot 2022-07-24 at 4 30 31 PM](https://user-images.githubusercontent.com/18497513/180644030-9994f070-1287-4503-b65a-f6c7dc72c63e.png)

Lets code:-

```
class Solution {
    public int[] smallestTrimmedNumbers(String[] nums, int[][] queries) {
        Map<Integer, int[]> map = new HashMap<>();
        int N = nums.length;
        int M = nums[0].length();
        int[][] tmp = new int[N][2];
        for(int c=0;c<N;c++){
            tmp[c][1] = c;
        }
        
        for(int i=0;i<M;i++){
            for(int j=0;j<N;j++){
                tmp[j][0] = nums[tmp[j][1]].charAt(M-1-i) - '0';
            }
            
            Arrays.sort(tmp, (a, b) -> {
                return a[0]-b[0];
            });
            
            int trans[] = new int[tmp.length];
            int ctr = 0;
            for(int tmpNum[]: tmp){
                trans[ctr++] = tmpNum[1];
            }
            
            map.put(i+1, trans);
        }
        
        int ans[] = new int[queries.length];
        int ctr = 0;
        for(int query[]: queries){
            ans[ctr++] = map.get(query[1])[query[0]-1];
        }
        
        return ans;
    }
}
```

Time complexity - O(MNlogN)
Space complexity - O(MN)
