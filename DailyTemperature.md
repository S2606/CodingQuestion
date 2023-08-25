## The question

Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.


Example 1:

```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```
```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```
```
Input: temperatures = [30,60,90]
Output: [1,1,0]
```

Intial Approach:- First preserve the original array position in a hashmap, then sort the array. sort the next greatest element in another hashmap. Iterate through the first array, find the next greatest, find their positions and get the answer. Time complexity - O(n log n). Can we do better?

Can use monotonic stack, how?

![LeetcodeDailyTemperature](https://github.com/S2606/CodingQuestion/assets/18497513/a4f2c13b-549e-433b-b812-a5f86e180365)

Code
```
int n = temperatures.length;
int res[] = new int[n];

Stack<Integer> st = new Stack<>();
for(int i = 0; i < n; i++)
{
    while(!st.isEmpty() && temperatures[i] > temperatures[st.peek()])
    {
        res[st.peek()] = i - st.peek();
        st.pop();
    }
    st.push(i);
}
return res;
```

Time complexity - O(n)
Space complexity - O(n)
