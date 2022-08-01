### The question

Design a food rating system that can do the following:

    Modify the rating of a food item listed in the system.
    Return the highest-rated food item for a type of cuisine in the system.

Implement the FoodRatings class:

    FoodRatings(String[] foods, String[] cuisines, int[] ratings) Initializes the system. The food items are described by foods, cuisines and ratings, all of which have a length of n.
        foods[i] is the name of the ith food,
        cuisines[i] is the type of cuisine of the ith food, and
        ratings[i] is the initial rating of the ith food.
    void changeRating(String food, int newRating) Changes the rating of the food item with the name food.
    String highestRated(String cuisine) Returns the name of the food item that has the highest rating for the given type of cuisine. If there is a tie, return the item with the lexicographically smaller name.

Note that a string x is lexicographically smaller than string y if x comes before y in dictionary order, that is, either x is a prefix of y, or if i is the first position such that x[i] != y[i], then x[i] comes before y[i] in alphabetic order.


Example 1:

```
["FoodRatings", "highestRated", "highestRated", "changeRating", "highestRated", "changeRating", "highestRated"]
[[["kimchi", "miso", "sushi", "moussaka", "ramen", "bulgogi"], ["korean", "japanese", "japanese", "greek", "japanese", "korean"], [9, 12, 8, 15, 14, 7]], ["korean"], ["japanese"], ["sushi", 16], ["japanese"], ["ramen", 16], ["japanese"]]
Output
[null, "kimchi", "ramen", null, "sushi", null, "ramen"]

Explanation
FoodRatings foodRatings = new FoodRatings(["kimchi", "miso", "sushi", "moussaka", "ramen", "bulgogi"], ["korean", "japanese", "japanese", "greek", "japanese", "korean"], [9, 12, 8, 15, 14, 7]);
foodRatings.highestRated("korean"); // return "kimchi"
                                    // "kimchi" is the highest rated korean food with a rating of 9.
foodRatings.highestRated("japanese"); // return "ramen"
                                      // "ramen" is the highest rated japanese food with a rating of 14.
foodRatings.changeRating("sushi", 16); // "sushi" now has a rating of 16.
foodRatings.highestRated("japanese"); // return "sushi"
                                      // "sushi" is the highest rated japanese food with a rating of 16.
foodRatings.changeRating("ramen", 16); // "ramen" now has a rating of 16.
foodRatings.highestRated("japanese"); // return "ramen"
                                      // Both "sushi" and "ramen" have a rating of 16.
                                      // However, "ramen" is lexicographically smaller than "sushi".
```

Approach:-
- Can use two HashMaps, one for mapping cusine to a Data structure for storing highest food rating(can use PriorityQueue)
- Another for mapping food name with another Data Structure(class) for maintaining food related information.

Code:-
```
class Food{
    String name; 
    int rating;
    String cuisine;
    
    public Food(String name, int rating, String cuisine){
        this.name=name;
        this.rating=rating;
        this.cuisine=cuisine;
    }
}

class FoodRatings {
    HashMap<String, PriorityQueue<Food>> x = new HashMap();
    HashMap<String, Food> menu = new HashMap();

    public FoodRatings(String[] foods, String[] cuisines, int[] ratings) {
        for(int i=0;i<foods.length;i++){
            Food food = new Food(foods[i], ratings[i], cuisines[i]);
            x.putIfAbsent(cuisines[i], new PriorityQueue<>((a, b) -> {
                if(b.rating==a.rating){
                    return a.name.compareTo(b.name);
                } else {
                    return b.rating-a.rating;
                }
            }));
            PriorityQueue<Food> pq = x.get(cuisines[i]);
            pq.add(food);
            menu.put(foods[i], food);
        }
    }
    
    public void changeRating(String food, int newRating) {
        Food foodObj = menu.get(food);
        PriorityQueue<Food> pq = x.get(foodObj.cuisine);
        pq.remove(foodObj);
        foodObj.rating = newRating;
        pq.add(foodObj);
    }
    
    public String highestRated(String cuisine) {
        return x.get(cuisine).peek().name;
    }
}
```

- Time complexity - O(nlogn)
- space complexity - O(n)
