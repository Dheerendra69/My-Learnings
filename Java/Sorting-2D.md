```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        int[][] arr = {
            {1, 3},
            {4, 1},
            {2, 2},
            {3, 2}
        };

        // sort by 2nd column ascending
        Arrays.sort(arr, Comparator.comparingInt(a -> a[1]));

        // sort by 1st column descending
        Arrays.sort(arr, (a, b) -> b[0] - a[0]);

        // sort by 1st column asc, then 2nd column asc
        Arrays.sort(arr, (a, b) -> {
            if (a[0] != b[0]) return a[0] - b[0];
            return a[1] - b[1];
        });
    }
}
```




