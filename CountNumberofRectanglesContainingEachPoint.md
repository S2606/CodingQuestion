### The question

You are given a 2D integer array rectangles where rectangles[i] = [li, hi] indicates that ith rectangle has a length of li and a height of hi. You are also given a 2D integer array points where points[j] = [xj, yj] is a point with coordinates (xj, yj).

The ith rectangle has its bottom-left corner point at the coordinates (0, 0) and its top-right corner point at (li, hi).

Return an integer array count of length points.length where count[j] is the number of rectangles that contain the jth point.

The ith rectangle contains the jth point if 0 <= xj <= li and 0 <= yj <= hi. Note that points that lie on the edges of a rectangle are also considered to be contained by that rectangle.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/165225268-646d9567-e8d8-4854-af1c-918b59ab42b4.png)

```
Input: rectangles = [[1,2],[2,3],[2,5]], points = [[2,1],[1,4]]
Output: [2,1]
Explanation: 
The first rectangle contains no points.
The second rectangle contains only the point (2, 1).
The third rectangle contains the points (2, 1) and (1, 4).
The number of rectangles that contain the point (2, 1) is 2.
The number of rectangles that contain the point (1, 4) is 1.
Therefore, we return [2, 1].
```

Approach:-

![Screenshot 2022-04-26 at 10 43 58 AM](https://user-images.githubusercontent.com/18497513/165226437-5ad37d39-692f-4905-9e06-8548dea607d6.png)

Lets code:-

```
public int binsearch(ArrayList<Integer> listX, int x){
    // Initializing last value here indicates that no boxes are greater than x
    int allMinNow = listX.size();
    int l = 0, r = listX.size()-1;
    while(l<=r){
        int mid = l + (r-l)/2;
        if(listX.get(mid) >= x) {
            allMinNow = mid;
            r = mid - 1;
        } else {
            l = mid + 1;
        }
    }

    return allMinNow;
}

public int[] countRectangles(int[][] rectangles, int[][] points) {
    HashMap<Integer, ArrayList<Integer>> map = new HashMap();
    for(int []rectangle: rectangles){
        if(map.containsKey(rectangle[1])){
            map.get(rectangle[1]).add(rectangle[0]);
        } else {
           ArrayList<Integer> arr = new ArrayList<Integer>();
           arr.add(rectangle[0]);
           map.put(rectangle[1], arr);   
        }
    }

    for(int y: map.keySet()){
        Collections.sort(map.get(y));
    }

    int[] ans = new int[points.length];
    for(int i=0;i<points.length;i++){
        int cnt = 0;
        int x = points[i][0];
        int y = points[i][1];

        for(int j = y; j <= 100; j++){
            if(map.containsKey(j)){
                ArrayList<Integer> listX = map.get(j);
                cnt += listX.size() - binsearch(listX, x);
            }   
        }

        ans[i] = cnt;
    }

    return ans;
}
```

Time complexity - O(m*100*log(n))
Space complexity - O(n)
