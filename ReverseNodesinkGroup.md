### The question

Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/163712471-c95ea0dd-4074-4514-bee3-caac16b5a15f.png)

```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

Approach:- 

```
In this approach, first we have considered taking additional memory(in the form of recursion stack). simply divide the code into two parts
1) List to be reversed
2) Remaining list which can further be sub-divided

Just process the first k-length list, followed by recursively call the next n-k length list, and cojoin them.

Time complexity - O(N)
Space complexity - O(N/k)
```

Lets code

```
public ListNode reverseLinkedList(ListNode head, int k) {
    ListNode new_head = null;
    ListNode ptr = head;

    while(k>0) {
        ListNode next_node = ptr.next;

        ptr.next = new_head;
        new_head = ptr;

        ptr = next_node;

        k--;
    }

    return new_head;
}

public ListNode reverseKGroup(ListNode head, int k) {
    int count = 0;
    ListNode ptr = head;

    while(count < k && ptr != null){
        ptr = ptr.next;
        count++;
    }

    if(count==k){
        ListNode reversedHead = this.reverseLinkedList(head, k);

        head.next = this.reverseKGroup(ptr, k);
        return reversedHead;
    }

    return head;
}
```

