**Goal:** Insert all elements of a 2-D array into a **min-heap**, comparing row elements.

### Case 1: Insert each element individually

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int[][] arr = {
            {3, 1, 4},
            {2, 8, 5}
        };

        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (int[] row : arr) {
            for (int val : row) {
                minHeap.add(val);
            }
        }

        while (!minHeap.isEmpty()) {
            System.out.print(minHeap.poll() + " ");
        }
    }
}
```

Min-heap compares values directly → smallest element always on top.

---

### Case 2: Treat each row as an element (compare row values)

Example: compare rows by **first element**

```java
PriorityQueue<int[]> minHeap = new PriorityQueue<>(
    Comparator.comparingInt(a -> a[0])
);

minHeap.add(new int[]{3, 1, 4});
minHeap.add(new int[]{2, 8, 5});
minHeap.add(new int[]{1, 9, 7});
```

---

### Case 3: Compare rows element-by-element (lexicographical)

```java
PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> {
    for (int i = 0; i < Math.min(a.length, b.length); i++) {
        if (a[i] != b[i]) return a[i] - b[i];
    }
    return a.length - b.length;
});
```

Rows are compared left to right, like dictionary order.
