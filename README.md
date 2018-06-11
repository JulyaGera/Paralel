# Paralel
Paralel OOP


Quick sort

Quicksort is a comparison sort, meaning that it can sort items of any type for which a "less-than" relation 
(formally, a total order) is defined. In efficient implementations it is not a stable sort, meaning that the 
relative order of equal sort items is not preserved. Quicksort can operate in-place on an array, requiring small
additional amounts of memory to perform the sorting. It is very similar to selection sort, except that it does
not always choose worst-case partition.

Mathematical analysis of quicksort shows that, on average, the algorithm takes O(n log n) comparisons to sort n items. 
In the worst case, it makes O(n2) comparisons, though this behavior is rare.

Algorithm

Quicksort is a divide and conquer algorithm. Quicksort first divides a large array into two smaller sub-arrays: 
the low elements and the high elements. Quicksort can then recursively sort the sub-arrays.

The steps are:

1.Pick an element, called a pivot, from the array.
2.Partitioning: reorder the array so that all elements with values less than the pivot come before the pivot,
while all elements with values greater than the pivot come after it (equal values can go either way). 
After this partitioning, the pivot is in its final position. This is called the partition operation.
3.Recursively apply the above steps to the sub-array of elements with smaller values and separately 
to the sub-array of elements with greater values.

The base case of the recursion is arrays of size zero or one, which are in order by definition, so they never need to be sorted.
The pivot selection and partitioning steps can be done in several different ways; the choice of specific
implementation schemes greatly affects the algorithm's performance



Parallelization

Quicksort's divide-and-conquer formulation makes it amenable to parallelization using task parallelism.
The partitioning step is accomplished through the use of a parallel prefix sum algorithm to compute an index 
for each array element in its section of the partitioned array. Given an array of size n, the partitioning
step performs O(n) work in O(log n) time and requires O(n) additional scratch space. 
After the array has been partitioned, the two partitions can be sorted recursively in parallel. 
Assuming an ideal choice of pivots, parallel quicksort sorts an array of size n in O(n log n) work in O(log² n)
time using O(n) additional space. 

Quicksort has some disadvantages when compared to alternative sorting algorithms, like merge sort,
which complicate its efficient parallelization. The depth of quicksort's divide-and-conquer tree directly
impacts the algorithm's scalability, and this depth is highly dependent on the algorithm's choice of pivot.
Additionally, it is difficult to parallelize the partitioning step efficiently in-place. 
The use of scratch space simplifies the partitioning step, but increases the algorithm's memory
footprint and constant overheads.



My personal experience and observations

When testing my program, I did it with small data arrays, the usual one-thread sorting works faster.
But already with large arrays (I had about 5000 elements or more), 4-thread sorting starts to work faster.
In this way, parallelization optimizes Quick sorting only with large amounts of data.
