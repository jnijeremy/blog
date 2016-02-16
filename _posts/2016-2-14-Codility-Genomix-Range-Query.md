---
layout: post
title: Codility Genomix Range Query

---

### [GenomicRangeQuery](https://codility.com/programmers/task/genomic_range_query/)

```
Given geno string and range query, find the minimal geno within the range.
"ACGT" = "1234"

e.g.
S = "CAGCCTA" # len = n
P = [2,5,0] # len = m
Q = [4,5,6]
result = [2,4,1]

S[2:5] = "GCC", min("GCC") = 2
S[5:6] = "T", min("T") = 4
S[0:7] = "CAGCCTA", min(S) = 1
```

### Solution O(n+m) Time, O(n) Space

Navie solution is to scan every range to find the minimal geno within the range.  This will end up in O(n*m) worst time (every range is the whole geno string).

The optimal idea is to keep a prefix sum for each geno at every position in S.  For range query [a,b], we can get the number of occurance of each geno in O(1) and get the smallest one.  Total run time is O(m + n), the prefixSum array takes O(N) space.

```
S = "CAGCCTA"
prefixArray = 
[
[0,1,0,0], #0
[1,1,0,0], #1
[1,1,1,0], #2
[1,2,1,0], #3
[1,3,1,0], #4
[1,3,1,1], #5
[2,3,1,1]  #6
]
```

```python
def genos(S, P, Q):
	n = len(S)
	m = len(P)
	prefixSum = [[0 for _ in range(4)] for _ in range(n)]
	result = [0 for _ in range(m)]
	d = {'A':1, 'C':2, 'G':3, 'T':4}
	
	# count every geno occurance
	for i,x in enumerate(S):
		prefixSum[i][d[x]-1] = 1
		
	# accumulate prefix sum
	for i in range(1, n):
		for j in tange(4):
			prefixSum[i][j] += prefixSum[i-1][j]
			
	# handle each query
	for i in range(m):
		x = P[i]
		y = Q[i]
		for geno in range(4):
			exist = 0
			if x > 0:
				exist = prefixSum[x-1][geno]
			if prefixSum[y][geno] - exist > 0:
				result[i] = geno + 1
				break
				
	return result
```