---
layout: post
title: Sorting Algorithms
update: 2016-2-19
excerpt: ""
---

#### Simple sorts

1. Insertion sort 

	O(n^2) Time, O(1) Space 

	Take the element one by one and inserting in their correct position into a new sorted list.

	![_config.yml]({{ site.baseurl }}/images/Insertion-sort-example-300px.gif)

2. Selection sort 

	O(n^2) Time, O(1) Space

	Find the minimum value, swap it with the vlaue in the first position and repeat these steps for the remainder of the list.
	
	![_config.yml]({{ site.baseurl }}/images/Selection-Sort-Animation.gif)
	
3. Bubble sort

	O(n^2) Time
	
	Start at the beginning of the data set, comapres the first two elements and if the first is greater than the second, it swaps them.  Continures doing this for each pair of adjacent elements to the end of the data set.  Start again with the first two elements, repeating until no swaps have occurred on the last pass.
	
	// can be used on a list of any length that is nearly sorted.
	
	![_config.yml]({{ site.baseurl }}/images/Bubble-sort-example-300px.gif)
	
	
#### Efficient sorts

1. Merge sort 

	O(nlogn) Time, O(n) Space

	Divide and concure.  Split the list into two parts, recursively sort them and then merge the sorted lists into a new list.
	
	![_config.yml]({{ site.baseurl }}/images/Merge-sort-example-300px.gif)
	
2. Heapsort

	O(nlogn) Time, O(n) Space
	
	Determining the largest (or smallest) element of the list, placing that at the end (or beginning) of the list, then continuing with the rest of the list.  The efficiency comes from the `heap` data structure.  Using a heap, finding the next largest element takes O(logn) time.

	![_config.yml]({{ site.baseurl }}/images/Heapsort-example.gif)

3. Quicksort

	O(nlogn) Average Time, O(n) Space
	
	![_config.yml]({{ site.baseurl }}/images/Quicksort-example.gif)
	
