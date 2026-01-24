


Good questions — these two details are the core of why this algorithm works and stays fast. Let’s break them down cleanly.

⸻

1️⃣ Why does r start from A.length?

We are doing binary search on the partition index i of array A, not on values.

What does i represent?

i = number of elements taken from A for the left half.

So valid values of i are:

0, 1, 2, ..., A.length

Why include A.length?

Because these are valid partitions:
	•	i = 0 → take 0 elements from A, all left-half elements come from B
	•	i = A.length → take all elements from A, remaining from B

If you set:

int r = A.length - 1;

you would miss the case where all elements of A are on the left side, which is a valid and sometimes necessary partition.

Binary search space

l = 0
r = A.length

means:

“Try every possible way of splitting A into left/right parts”

That’s exactly what we need.

⸻

2️⃣ Why do we always pick the smaller array for binary search?

This is both for correctness and performance.

⸻

✅ Reason 1: To keep j in valid bounds

Recall:

j = half - i

If we binary-search the larger array, i can get large, which can make:

j < 0  OR  j > B.length

That leads to invalid indexing in array B.

By choosing A as the smaller array:

0 ≤ i ≤ A.length
⇒ j always stays within [0, B.length]

So we never access out-of-range elements.

⸻

✅ Reason 2: Guaranteed O(log(min(n, m))) time

Binary search runs in:

O(log(size of searched array))

If you search the larger array:

O(log(max(n, m)))

If you search the smaller array:

O(log(min(n, m)))  ← optimal and required by the problem

This is exactly why LeetCode expects this approach.

⸻

✅ Reason 3: Cleaner edge-case handling

When A is smaller:
	•	Empty array case (A.length == 0) works naturally
	•	Infinity boundaries (±∞) handle edges safely
	•	No extra condition checks needed

If you don’t do this swap, your code becomes much more complex and bug-prone.

⸻

Mental model (important)

Think of it like this:

We are choosing how many elements to take from A
B automatically adjusts to complete the left half
So we search where the choice space is smallest

⸻

TL;DR

🔹 Why r = A.length?

Because i is a partition index, and all values from 0 to A.length are valid.

🔹 Why binary search the smaller array?
	•	Keeps j always valid
	•	Guarantees O(log(min(n, m)))
	•	Avoids ugly edge cases

If you want, I can also:
	•	Walk through a dry run with numbers
	•	Show what breaks if you search the bigger array
	•	Explain this visually (partition diagram style)

Just say 👍

