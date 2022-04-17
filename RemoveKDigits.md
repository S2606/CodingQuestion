### The question

Given string num representing a non-negative integer num, and an integer k, return the smallest possible integer after removing k digits from num.

Example 1:

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

Approach:-

<img width="722" alt="Screenshot 2022-04-17 at 4 40 40 PM" src="https://user-images.githubusercontent.com/18497513/163711893-9da28519-9136-4299-913b-4ffacde1b98c.png">

Lets code:-

```
public String removeKdigits(String num, int k) {
    LinkedList<Character> stk = new LinkedList<Character>();
    for(char c: num.toCharArray()){
        while(stk.size() > 0 && k > 0 && stk.peekLast() > c){
            stk.removeLast();
            k-=1;
        }
        stk.addLast(c);
    }

    for(int i=0;i<k;++i){
        stk.removeLast();
    }

    StringBuilder sb = new StringBuilder();
    boolean leadingZero = true;
    for(char c: stk){
        if(leadingZero && c=='0') continue;
        leadingZero = false;
        sb.append(c);
    }

    if(sb.length()==0) return "0";
    return sb.toString();
}
```

Time complexity - O(N)
Space complexity - O(N)
