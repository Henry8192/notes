# Balance Sorted List
Write a Python function that consumes two non-empty sorted lists of integers of equal sizes and returns a list of two natural numbers `[i, j]` such that if `L[i]` and `M[j]` were swapped in the lists, then the sums of the integers in L and M would be equal. If there are multiple such indices, choose the pair with the smallest value of i (and then if there is a tie with j indices, choose the smallest j index corresponding to the smallest i index). If no such indices exist, return None.
- For 80% of the grade for auto-testing, your code can run in any time.
- For the remaining 20% of the grade for auto-testing, your code must run in $O(n)$ time where n is the length of either list.

## Hint
Think about what condition involving the two lists and return values needs to be true.

##Samples:

	balance_sorted_lists([245543], [245544]) => None
	balance_sorted_lists([-3, 1, 2, 3], [6, 7, 8, 12]) => [0, 3]
	balance_sorted_lists([1, 3, 3, 4, 6, 8, 8, 8, 10], [1, 1, 2, 2, 7, 7, 7, 7, 15]) => [1, 2]
