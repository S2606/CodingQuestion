### The question

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

Example 1:

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

Approach:-
```
Remember backward-rowing?? Can use the same concept here as well. How??

All you need to do is row on one side, find elements product at that particular side)excluding the number), and then jyst simply do it on the other side
as well?

Eg:- [1,2,3,4]
Now lets row from right-to-left side. In this since we know that there are no elements to right of 4, we consider it as 1

[1,2,3,1]
Now at 3, the answer will be 4 since product at the right side of 3 except considering the number 3 is 1*4(since 4 is the number that will be considered)

[1,2,4,1]
Now at 3, the answer will be 12 since product at the right side of 2 except considering the number 2 is 4*3(since 3 is the number that will be considered, 
and 4 is the product found till index n+2)

[1,12,4,1]
Now at 1, the answer will be 24 since product at the right side of 1 except considering the number 1 is 12*2(since 2 is the number that will be considered, 
and 12 is the product found till index n+2)

[24,12,4,1]

Now lets go to opposite side, but there will be similar rules

[24,12,4,1]
Now lets row from left-to-right side. In this since we know that there are no elements to left of 1, we consider it as 1

[24,12,4,1]
Now at index 1, the answer will be 1 since product at the left side of index 1 except considering the element is 1*1(since 1 is the number that will be considered)

[24, 12, 4, 1]
Now at index 2, the answer will be 8 since product at the left side of index 2 except considering the element is 2*4(since 2 is the number that will be considered)

[24, 12, 8, 1]
Now at index 3, the answer will be 6 since product at the left side of index 3 except considering the element is 1*6(since 3 is the number that will be considered)

[24, 12, 8, 6]
```

Lets code
```
public int[] productExceptSelf(int[] nums) {
    int n = nums.length;
    int outputArray[] = new int[n];

    outputArray[n-1] = 1;
    outputArray[n-2] = nums[n-1];
    for(int i=n-3; i>=0; i--){
        outputArray[i] = nums[i+1] * outputArray[i+1];
    }


    int leftProd = 1;
    for(int i=1; i<n; i++){
        leftProd *= nums[i-1];
        outputArray[i] = leftProd * outputArray[i];
    }

    return outputArray;
}
```

Time complexity - O(n)
Space complexity - O(n)
