## The question

You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a triple booking.

A triple booking happens when three events have some non-empty intersection (i.e., some moment is common to all the three events.).

The event can be represented as a pair of integers start and end that represents a booking on the half-open interval [start, end), the range of real numbers x such that start <= x < end.

Implement the MyCalendarTwo class:

    MyCalendarTwo() Initializes the calendar object.
    boolean book(int start, int end) Returns true if the event can be added to the calendar successfully without causing a triple booking. Otherwise, return false and do not add the event to the calendar.

Example 1:
```
Input
["MyCalendarTwo", "book", "book", "book", "book", "book", "book"]
[[], [10, 20], [50, 60], [10, 40], [5, 15], [5, 10], [25, 55]]
Output
[null, true, true, true, false, true, true]

Explanation
MyCalendarTwo myCalendarTwo = new MyCalendarTwo();
myCalendarTwo.book(10, 20); // return True, The event can be booked. 
myCalendarTwo.book(50, 60); // return True, The event can be booked. 
myCalendarTwo.book(10, 40); // return True, The event can be double booked. 
myCalendarTwo.book(5, 15);  // return False, The event cannot be booked, because it would result in a triple booking.
myCalendarTwo.book(5, 10); // return True, The event can be booked, as it does not use time 10 which is already double booked.
myCalendarTwo.book(25, 55); // return True, The event can be booked, as the time in [25, 40) will be double booked with the third event, the time [40, 50) will be single booked, and the time [50, 55) will be double booked with the second event.
```

Approach:- First thought of something related to two treemaps, one for storing single bookings and another for storing double bookings(will share the solution below), but then i thought why not extend it in such a way that we need only one treemap and tomorrow if we get a requirement for allowing n overlapping bookings? Although the trade-off would be for time since the second solution does have sorting element to it.

- First solution basically is to have two lists, one for single bookings and another for double bookings. Basically while iterating both the lists, have the same checks in place(lets assume booking[] as the name of the two-size array storing the start and end in the list)
```
booking[0]<end && booking[1]>start
```
if the above check is done for double bookings list, it simply means there is a case of triple booking which means it cannot be considered, hence marked false. On the other hand, if this check is done for single booking list, it means that check leads to a new entry in double booking, with start as max of booking[0] ans start and end shall be min of booking[1] and end.

Code
```
private final List<int[]> bookings;
private final List<int[]> doubleBookings;

public MyCalendarTwo() {
    this.bookings = new ArrayList<>();
    this.doubleBookings = new ArrayList<>();
}

public boolean book(final int start, final int end) {
    for(final int[] booking : doubleBookings)
        if(booking[0] < end && booking[1] > start)
            return false;

    for(final int[] booking : bookings)
        if(booking[0] < end && booking[1] > start)
            doubleBookings.add(new int[] { Math.max(start, booking[0]), Math.min(end, booking[1]) });

    bookings.add(new int[] { start, end });
    return true;
}
```
Time complexity - O(n)
Space complexity - O(n)

- Second solution is quite clever if you think about it. So instead of having two lists, how about one sorted list that contains occurence of the element as the value and the element itself as the key, Okay how does the algo work then?

![image](https://github.com/user-attachments/assets/8fdec0da-36cc-4b0d-a456-870414fde192)

Code
```
class MyCalendarTwo {

    private final TreeMap<Integer, Integer> calendar;

    public MyCalendarTwo() {
        this.calendar = new TreeMap<>();
    }
    
    public boolean book(final int start, final int end) {
        calendar.put(start, calendar.getOrDefault(start, 0) + 1);
        calendar.put(end, calendar.getOrDefault(end, 0) - 1);

        int events = 0;

        for(final int val : this.calendar.values()) {
            events += val;

            if(events > 2) {
                this.calendar.put(start, this.calendar.get(start) - 1);
                this.calendar.put(end, this.calendar.get(end) + 1);

                if(this.calendar.get(start) == 0)
                    this.calendar.remove(start);

                if(this.calendar.get(end) == 0)
                    this.calendar.remove(end);

                return false;
            }
        }

        return true;
    }
}
```
Time complexity - O(nlogn) because treemap inherently does the sorting part with keys of the map  
Space complexity - O(n)

