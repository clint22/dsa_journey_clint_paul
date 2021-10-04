# dsa_journey_clint_paul
## 1. Sales by Match 
**Site: HackerRank\
Difficulty: Easy\
Language: Kotlin**

There is a large pile of socks that must be paired by color. Given an array of integers representing the color of each sock, determine how many pairs of socks with matching colors there are.

**Example**\
**n = 7**\
**ar = [1,2,1,2,1,3,2]**\
There is one pair of color 1 and one of color 2. There are three odd socks left, one of each color. The number of pairs is 2.

**Soultion**

```
fun sockMerchant(n: Int, ar: Array<Int>): Int {
   var totalNoOfPairs = 0
    for (i in 0 until n) {
        if (ar[i] != 0) {
            for (j in i + 1 until n) {
                if (ar[i] == ar[j]) {
                    totalNoOfPairs++
                    ar[j] = 0
                    break
                }
            }
        }

    }
    return totalNoOfPairs
}
```
**Explanation**

This seems like a very simple problem. The easiest approach is to do a brute force search using a nested loop and keep a counter to add the number of pairs. Well there is one small problem. Since, we are finding the no.of pairs from the array, the array will most probably contains a **duplication**. So, the chances are that we might increment the **totalNoOfPairs** counter unknowingly by comparing the already compared socks with other.\
Let's explain it through an example.\
Sample array: [1,2,1,2,1,3,2]
```
1. When i[0] = 1 & j[1] = 2 -> i[0] != j[1] -> counter = 0
2. When i[0] = 1 & j[2] = 1 -> i[0] = j[2] -> counter = 1 
3. *break the loop* 
4. When i[1] = 2 & j[2] = 1 -> i[1] != j[2] -> counter = 1 
5. When i[1] = 2 & j[3] = 2 -> i[1] = j[3] -> counter = 2 
6. *break the loop* 
7. When i[2] = 1 & j[3] = 2 -> i[2] != j[3] -> counter = 2 ( *Seems like this is not correct no? We have already added this sock as a pair right?*)
8. When i[2] = 1 & j[4] = 1 -> i[2] = j[4] -> counter = 3
9. **ERROR** -> We already know that there are only 2 pairs of socks in the given array. But, the counter already is 3. Why? Because we are checking the sock we already checked before. 
```

How to solve this small issue? Simple. Just make sure you are modifying the array item with a '0' value whenever you find a matching pair. And, then, you can skip the array element with the '0' value when you check for the pairs.\
Let's explain it through an example.\
Sample array: [1,2,1,2,1,3,2]
```
1. When i[0] = 1 -> Check if i[0] != 0
2. When i[0] = 1 & j[1] = 2 -> i[0] != j[1] -> counter = 0
3. When i[0] = 1 & j[2] = 1 -> i[0] = j[2] -> counter = 1 
4. Set j[2] as 0.
5. *break the loop* 
6. Modified array = [1,2,0,2,1,3,2]
7. When i[1] = 2 -> Check if i[1] != 0
8. When i[1] = 2 & j[2] = 0 -> i[1] != j[2] -> counter = 1 
9. When i[1] = 2 & j[3] = 2 -> i[1] = j[3] -> counter = 2 
10. Set j[3] as 0.
11. Modified array = [1,2,0,0,1,3,2]
12. *break the loop*
13. When i[2] = 0 -> Check if i[2] != 0 
14. Since i[2] is 0 then we can skip this case. 
15. When i[3] = 0 -> Check if i[3] != 0 
16. Since i[3] is 0 then we can skip this case as well. 
17. when i[4] = 1 -> Check if i[4] != 0 
18. When i[4] = 1 & j[5] = 3 -> i[4] != j[5] -> counter = 2 
19. When i[4] = 1 & j[6] = 2 -> i[4] != j[6] -> counter = 2 
20. When i[5] = 3 & j[6] = 2 -> i[5] != j[6] -> counter = 2 
```
That's all. 😄
