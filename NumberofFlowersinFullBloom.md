### The question

You are given a 0-indexed 2D integer array flowers, where flowers[i] = [starti, endi] means the ith flower will be in full bloom from starti to endi (inclusive). You are also given a 0-indexed integer array persons of size n, where persons[i] is the time that the ith person will arrive to see the flowers.

Return an integer array answer of size n, where answer[i] is the number of flowers that are in full bloom when the ith person arrives.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/165417268-02e74c82-d236-4ee4-b650-cc5d57d14f47.png)

```
Input: flowers = [[1,6],[3,7],[9,12],[4,13]], persons = [2,3,7,11]
Output: [1,2,2,2]
Explanation: The figure above shows the times when the flowers are in full bloom and when the people arrive.
For each person, we return the number of flowers in full bloom during their arrival.
```

Approach:- 
```
Initially had tried this approach

public int[] fullBloomFlowers(int[][] flowers, int[] persons) {
    int n = persons.length;
    HashSet<Integer> personSet = new HashSet<Integer>();
    int maxPersonTime = 0;
    for(int person: persons){
        personSet.add(person);
        maxPersonTime = Math.max(maxPersonTime, person);
    }
    HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
    for(int []flower: flowers){
        for(int start=flower[0]; start<=Math.min(flower[1], maxPersonTime); start++){
            if(personSet.contains(start)){
                map.put(start, map.getOrDefault(start, 0)+1);
            }
        }
    }

    int[] resp = new int[n];
    for(int i=0;i<n;i++){
        resp[i] = map.getOrDefault(persons[i], 0);
    }

    return resp;
}

But it did fail, reason being large input set was not considered. So this problem falls in the classic range of Segment Trees/ Range Query related problem.
In this we first need to calculate the box in the diagram above, How??

Have an map(TreeMap in this case), if a flower is found at position start, increment it(indication of a bloomed flower), else if flower has exceeded its bloom time, decrement it(time would be end +1). 

![Screenshot 2022-04-27 at 6 44 35 AM](https://user-images.githubusercontent.com/18497513/165418597-969b1c94-d202-4511-9059-6811f522d260.png)

Then just simply do a binary search on time t for each person
```

Lets code
```
public int[] fullBloomFlowers(int[][] flowers, int[] persons) {
    TreeMap<Integer, Integer> treeMap = new TreeMap<Integer, Integer>();
    for(int flower[]: flowers){
        treeMap.put(flower[0], treeMap.getOrDefault(flower[0], 0)+1);
        treeMap.put(flower[1]+1, treeMap.getOrDefault(flower[1]+1, 0)-1);
    }

    TreeMap<Integer, Integer> sum = new TreeMap<Integer, Integer>();
    int prev = 0;
    for(Map.Entry<Integer, Integer> entry: treeMap.entrySet()){
        prev += entry.getValue();
        sum.put(entry.getKey(), prev);
    }

    int n = persons.length;
    int result[] = new int[n];
    for(int i=0;i<n;i++){
        //floorEntry will give the greatest value less than or equal to key k
        Map.Entry<Integer, Integer> entry = sum.floorEntry(persons[i]);
        if(entry != null){
            result[i] = entry.getValue();
        }
    }

    return result;
}
```
Time complexity - O(nlogm+mlogn)
Space complexity - O(n)
