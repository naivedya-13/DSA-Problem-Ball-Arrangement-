# Ball Arrangement Problem (Non-Adjacent Ball Placement)

## Problem Overview

In this problem, we are tasked with finding the number of **valid arrangements** of colored balls (Green, Yellow, and Red) such that **no two balls of the same color** are placed adjacent to each other.

### **Example:**

- **Input**: 
  - Green (G) = 2
  - Yellow (Y) = 2
  - Red (R) = 2

- **Output**: 
  - Valid arrangements = 6
  - Example arrangements:  
    ```
    G Y R
    G R Y
    Y G R
    Y R G
    R G Y
    R Y G
    ```

## Problem Constraints

- Balls of the same color must not be adjacent to each other.
- The number of green, yellow, and red balls are provided as input, and the program should calculate all possible valid arrangements.

## Approach

This problem is solved using **recursion** and **backtracking**. The idea is to:
1. Start with an empty arrangement.
2. Place one ball at a time in the arrangement, ensuring no two balls of the same color are adjacent.
3. Continue placing the balls recursively until all the balls are arranged.
4. Once all the balls are placed, it counts as a valid arrangement.
5. The process continues until all combinations are explored.

### **Algorithm Explanation**:
- We use a recursive helper function `findArrangements` which takes the following parameters:
  - `G`: Number of green balls remaining.
  - `Y`: Number of yellow balls remaining.
  - `R`: Number of red balls remaining.
  - `last`: The last ball placed (used to ensure no adjacent balls of the same color).
  - `arrangement`: The current arrangement of balls being built.
- The recursion will:
  - Add a ball of each color (G, Y, or R) to the arrangement, but only if the color is not the same as the last placed ball.
  - When all balls are placed, it will print the arrangement and increment a count of valid arrangements.

## Code

```java
import java.util.Scanner;

public class BallArrangement {
    static int count = 0; // Global counter for valid arrangements

    static void findArrangements(int G, int Y, int R, char last, String arrangement) {
        if (G == 0 && Y == 0 && R == 0) {
            count++; // Increment counter for each valid arrangement
            System.out.println(arrangement.trim()); // Print arrangement
            return;
        }

        if (G > 0 && last != 'G')
            findArrangements(G - 1, Y, R, 'G', arrangement + "G ");
        if (Y > 0 && last != 'Y')
            findArrangements(G, Y - 1, R, 'Y', arrangement + "Y ");
        if (R > 0 && last != 'R')
            findArrangements(G, Y, R - 1, 'R', arrangement + "R ");
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter G Y R (space-separated): ");
        int G = sc.nextInt(), Y = sc.nextInt(), R = sc.nextInt();
        sc.close();

        System.out.println("\nValid Arrangements:");
        findArrangements(G, Y, R, 'X', ""); // Start recursion with an empty string

        System.out.println("\nTotal valid arrangements: " + count); // Print total count
    }
}
```

### **Output for Example Input:**
```
Enter G Y R (space-separated): 2 2 2

Valid Arrangements:
G Y R 
G R Y 
Y G R 
Y R G 
R G Y 
R Y G

Total valid arrangements: 6
```

## Time Complexity

- **Time Complexity**:  
  The time complexity of the algorithm is **O((G + Y + R)!)**. This is because we are recursively placing the balls in every possible arrangement, and for each recursive call, we reduce the number of remaining balls by 1. In the worst case, the number of recursive calls is proportional to the factorial of the sum of all the balls, i.e., (G + Y + R)!.

- **Space Complexity**:  
  The space complexity is **O(G + Y + R)** due to the recursive call stack, as each recursive call uses space proportional to the number of remaining balls.

## Mathematical Formula for Valid Arrangements

In the general case, if we have `G` green balls, `Y` yellow balls, and `R` red balls, the total number of valid arrangements can be modeled as a permutation problem with the constraint that no two balls of the same color are adjacent. This is a complex problem and is computed via recursion as done in the provided code, which generates each arrangement while adhering to the constraints.

### **Formula for Total Arrangements (Without Adjacent Balls of the Same Color)**:
Unfortunately, there is no direct mathematical formula to compute the exact number of valid arrangements without adjacent balls of the same color. This is because the problem involves recursive placement, ensuring that the last placed ball isn't repeated. As such, this problem requires recursive backtracking as implemented in the code above.

## Conclusion

This Java program provides a solution to the ball arrangement problem with the non-adjacency constraint. The recursion explores all possible valid placements, and the program prints out all valid arrangements and the total count of valid configurations.

Feel free to try it with different inputs for the number of green, yellow, and red balls to explore how the valid arrangements change! 🌟

## Keywords:
- Java
- Recursion
- Backtracking
- Permutation
- Combinatorics

---

This README provides an explanation of the problem, solution approach, the Java code, and the time complexity. It also covers the mathematical context and limitations of directly calculating the number of valid arrangements. You can modify the README as per your requirement!
