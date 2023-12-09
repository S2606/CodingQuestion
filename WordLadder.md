## The question

A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s1 -> s2 -> ... -> sk such that:

    Every adjacent pair of words differs by a single letter.
    Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
    sk == endWord

Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.

Example 1:

Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

Example 2:

Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.

Constraints:

    1 <= beginWord.length <= 10
    endWord.length == beginWord.length
    1 <= wordList.length <= 5000
    wordList[i].length == beginWord.length
    beginWord, endWord, and wordList[i] consist of lowercase English letters.
    beginWord != endWord
    All the words in wordList are unique.

Approach:- 

Since it is saying shortest transformation sequence, and the heuristic way is to traverse from one word to another, BFS was something had thought of. But how do we preprocess the graph creation part?

![Screenshot 2023-12-09 at 5 29 53 PM](https://github.com/S2606/CodingQuestion/assets/18497513/cf10acf0-9ad7-4d77-9056-2dd29d3af74b)

Code:-

```
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        int L = beginWord.length();
        Map<String, List<String>> allComboDict = new HashMap<String, List<String>>();
        wordList.forEach(word -> {
            for(int i=0;i<L;i++){
                String intermediary = word.substring(0, i) + "*" + word.substring(i+1, L);
                List<String> allComboList = allComboDict.getOrDefault(intermediary, new ArrayList<String>());
                allComboList.add(word);
                allComboDict.put(intermediary, allComboList);
            }
        });
        Queue<Pair<String, Integer>> queue = new LinkedList<>();
        queue.add(new Pair(beginWord, 1));

        Map<String, Boolean> visited = new HashMap<>();
        while(!queue.isEmpty()){
            Pair<String, Integer> ele = queue.poll();
            String word = ele.getKey();
            Integer level = ele.getValue();

            if(visited.containsKey(word)){
                continue;
            }
            visited.put(word, true);
            for(int i=0;i<L;i++){
                String intermediary = word.substring(0, i) + "*" + word.substring(i+1, L);
                if(allComboDict.containsKey(intermediary)){
                    List<String> allComboList = allComboDict.get(intermediary);
                    for(String combo: allComboList){
                        if(combo.equals(endWord)){
                            return level+1;
                        }
                        queue.add(new Pair(combo, level+1));
                    }
                }
            }
        }

        return 0;
    }
}
```

Complexities:-

Time:- O(M^2*N), 
How? 
- So in the first half of the code, assuming M is the length of word and N is total number of words, M*N. But note that we are perfoming substring operation(for creation of a new string)as well which shall cost another O(M) operation as well. Hence O(M^2*N)
- in the second half, assuming worst case in which we need to traverse all words, queue size can be N taking the previous definitions into consideration. for each word we traverse M times, and another M times for the same reason(substring operation) above. Hence O(M^2*N)
Hence final time complexity is O(M^2*N)

Space:- O(M^2*N),
How?
- for each word we shall have M intermediary words created. in allComboDict for each intermediary word, we store original word of length M. So total space for each word would be O(M^2). For N words, it shall be O(M^2*N).
- the queues and hashMap shall take O(M*N). But we always consider larger space complexity in our equation. Hence O(M^2*N).




