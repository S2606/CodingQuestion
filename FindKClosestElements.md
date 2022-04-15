### The question

Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:

    |a - x| < |b - x|, or
    |a - x| == |b - x| and a < b

Example 1:

```
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]
```

Approach:-

![Screenshot 2022-04-15 at 7 16 58 PM](https://user-images.githubusercontent.com/18497513/163578460-7c79a43e-c300-423d-ac5f-1fe729792511.png)

Lets code

```
public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int left = 0, right = arr.length - k;
    while(left<right){
        int mid = (left + right)/2;
        if(x-arr[mid] > arr[mid+k]-x){
            left = mid + 1;
        } else {
            right = mid;
        }
    }

    return Arrays.stream(arr, left, left+k).boxed().collect(Collectors.toList());
}
```

Time complexity - O(log(N-K)) where N is length of array
Space complexity - O(K)
