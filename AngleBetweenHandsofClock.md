### The question

Given two numbers, hour and minutes, return the smaller angle (in degrees) formed between the hour and the minute hand.

Answers within 10-5 of the actual value will be accepted as correct.

Example 1:

![image](https://user-images.githubusercontent.com/18497513/159125637-d6257f20-aca2-484d-867d-9a3839bf84f4.png)

```
Input: hour = 12, minutes = 30
Output: 165
```

Approach:- 

![Screenshot 2022-03-19 at 8 43 04 PM](https://user-images.githubusercontent.com/18497513/159126761-fc7f5a05-0c4b-421e-b0ae-d8050575d501.png)

Code 

```
 public double angleClock(int hour, int minutes) {
    int oneMinAngle = 6;
    int oneHourAngle = 30;
    
    double minuteAngle = minutes * oneMinAngle;
    double hourAngle = ((hour%12)+minutes/60.0) * oneHourAngle;
    
    doubel diff = Math.abs(hourAngle - minuteAngle);
    return Math.min(diff, 360-diff);
}
```

Time complexity - O(1)
Space complexity - O(1)
