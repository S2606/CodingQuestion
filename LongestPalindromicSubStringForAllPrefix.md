### The question

Given a String like "ababa", the lengths of the longest palindromic substrings for all the prefixes will be as per below -

    "a" : "a" (Length 1)
    "ab" : "a" or "b" (Length 1)
    "aba" : "aba" (Length 3)
    "abab" : "aba" or "bab" (Length 3)
    "ababa" : "ababa" (Length 5)

Here's the sample input / output ->

    Sample Input: "ababa"
    Sample Output: 1 1 3 3 5

Approach:-

![Screenshot 2023-10-20 at 6 58 41 AM](https://github.com/S2606/CodingQuestion/assets/18497513/42e27621-ff03-4dd6-be0b-b85a418f9d8f)

Code:-
```
public int[] longestPalindrome(String s) {
    int n = s.length();
    boolean palindrome[][] = new boolean[n][n];
    int palindromeLen[][] = new int[n][n];

    for(int g=0;g<n;g++){
        for(int i=0, j=g;j<n;i++, j++){
            if(g==0){
                palindrome[i][j] = true;
                palindromeLen[i][j] = 1;
            } else if(g==1){
                if(s.charAt(i)==s.charAt(j)){
                    palindrome[i][j] = true;
                    palindromeLen[i][j] = 2;
                } else {
                    palindrome[i][j] = false;
                    palindromeLen[i][j] = 1;
                }
            } else {
                if(s.charAt(i)==s.charAt(j) && palindrome[i+1][j-1]){
                    palindrome[i][j] = true;
                    palindromeLen[i][j] = palindromeLen[i+1][j-1]+2;
                } else {
                    palindrome[i][j] = false;
                    palindromeLen[i][j] = palindromeLen[i+1][j-1];
                }
            }
        }
    }

    int[] result = new int[n];
    int maxTillNow = 1;
    for(int i=0;i<n;i++) {
        if(maxTillNow < palindromeLen[0][i]) {
            maxTillNow = palindromeLen[0][i];
        }
        System.out.println(maxTillNow);
        result[i] = maxTillNow;
    }

    return result;
}
```

Time complexity = O(n^2)

Space complexity  = O(2*n^2)
