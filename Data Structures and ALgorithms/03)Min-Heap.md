How to  create a custom comparator for a min-heap?

In Java, a min-heap is usually created using PriorityQueue.
You control the heap order by giving it a custom Comparator.

Let’s break it down cleanly 👇

⸻

1️⃣ Basic syntax (custom comparator)

PriorityQueue<T> pq = new PriorityQueue<>(
    (a, b) -> /* comparison logic */
);

👉 Rule:
	•	return negative → a comes before b
	•	return 0 → equal
	•	return positive → b comes before a

⸻

2️⃣ Min-heap for integers (custom logic)

Example: Min-heap based on absolute value

PriorityQueue<Integer> pq = new PriorityQueue<>(
    (a, b) -> Math.abs(a) - Math.abs(b)
);

🧠 Smaller absolute value = higher priority

⸻

3️⃣ Min-heap for custom objects

Example class

class Pair {
    int x;
    int y;

    Pair(int x, int y) {
        this.x = x;
        this.y = y;
    }
}


⸻

Min-heap based on x

PriorityQueue<Pair> pq = new PriorityQueue<>(
    (a, b) -> a.x - b.x
);

⚠️ Overflow safe version (recommended):

PriorityQueue<Pair> pq = new PriorityQueue<>(
    (a, b) -> Integer.compare(a.x, b.x)
);


⸻

4️⃣ Multiple conditions (very common in DSA 🔥)

Min-heap by x, tie-break by y

PriorityQueue<Pair> pq = new PriorityQueue<>(
    (a, b) -> {
        if (a.x != b.x)
            return Integer.compare(a.x, b.x);
        return Integer.compare(a.y, b.y);
    }
);

🧠 This is super useful in:
	•	Dijkstra
	•	K closest points
	•	Scheduling problems
	•	Greedy algorithms

⸻

5️⃣ Using Comparator class (cleaner for big logic)

PriorityQueue<Pair> pq = new PriorityQueue<>(
    new Comparator<Pair>() {
        @Override
        public int compare(Pair a, Pair b) {
            return Integer.compare(a.x, b.x);
        }
    }
);


⸻

6️⃣ Max-heap vs Min-heap reminder

Java’s PriorityQueue is min-heap by default.

Max-heap using comparator:

PriorityQueue<Integer> maxHeap = new PriorityQueue<>(
    (a, b) -> b - a
);


⸻

7️⃣ Real DSA example (Dijkstra)

PriorityQueue<int[]> pq = new PriorityQueue<>(
    (a, b) -> Integer.compare(a[1], b[1]) // min distance
);

int[] = {node, distance}

⸻

💡 Pro tip (you’ll like this as a DSA grinder 😄)

Always use:

Integer.compare(a, b)

instead of:

a - b

to avoid overflow bugs in edge cases.




