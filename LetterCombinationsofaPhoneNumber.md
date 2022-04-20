Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example 1:

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

Approach:-
```
Simply just take a character from set of digits, check the size of output list with current character position(this would mean string of that size 
is being made). once checked for equality just pull the string S`, find out number's mapping with the corresponding string(2->"abc"), pluck
out each character and append to string S`.

23
List = ['']

Since list has string of size 0 which is equal to first element's index(zero-indexed), add a, b, c

List = ['a', 'b', 'c']

Now for 3 since string of size 1 which is equal to second element's index(zero-indexed), add d,e,f such that

List = ['ad', 'ae', 'af', 'b', 'c']
List = ['ad', 'ae', 'af', 'bd', 'be', 'bf', 'c']
List = ['ad', 'ae', 'af', 'bd', 'be', 'bf', 'cd', 'ce', 'cf']
```

Lets code
```
public List<String> letterCombinations(String digits) {
    LinkedList<String> result = new LinkedList<String>();
    if(digits.length()==0){
          return result;
    }
    result.add("");
    
    String []numbers = new String[]{"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    
    for(int i=0;i<digits.length;i++){
        int num = Character.getNumericValue(digits.charAt(i));
        while(result.peek().length()==i){
          String premut = result.remove();
          for(char c: numbers[num].toCharArray()){
              result.add(premut+c);
          }
        }
    }
    
    return result;
}
```

Time complexity - O(4^N) since 4 is the maximum size of the input
Space complexity - O(4^N)
