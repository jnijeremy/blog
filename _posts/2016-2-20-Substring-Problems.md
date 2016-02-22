---
layout: post
title: Substring Problems
update: 2016-2-22
excerpt: <p>A collection of problems about finding some special longest substing</p>

---

## Problem 1

[Find the longest substring with k unique characters in a given string](http://www.geeksforgeeks.org/find-the-longest-substring-with-k-unique-characters-in-a-given-string/)

[Leetcode #159 Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

> Given a string you need to print longest possible substring that has exactly M unique characters. If there are more than one substring of longest possible length, then print any one of them.


### Brute Force Solution

Algorithm:

Loop through each index, find the longest valid substirng starting from that index.  Takes O(N^2) time and O(k) space.

Optimize:

1. Can be improved by skipping some index ( e.g. `aaa` only the first `a` needs to be considered ).  Same worst case time. 

2. Can be further improved if using an iterative updating approach and store extra information for possible starting indexes.

	Algorithm:
	
	Loop through every potential starting index, for each index, store the current valid substring length and all current letters in a hash map for that index.  For each index, also update all the previous index that needs to be updated.  For previous indexes that will exceed k unique letters, fix them and they don't need to be updated in the future.
	
	Analysis:
	
	Worst case is when all previous indexes need to be updated, giving O(N^2).  Average time is improved because we skip index once they reach their limit.  However, each index now takes at most O(k) memory, the total memory cost is O(N*k).
	
	e.g.
	
	```
	aabacbebebe, k = 2
	
	step1: a // 1 {a:1}
	
	step2: a | a // 2 {a:2} | null
	
	step3: a | a | b // 3 {a:2, b:1} | null | 1 {b:1}
	
	step4: a | a | b | a
	
	4 {a:3, b:1} | null | 2 {b:1, a:1} | 1 {a:1}
	
	step5: a | a | b | a | c
	
	fixed 4 {a:3, b:1} | fixed null | fixed 2 {b:1, a:1} | 2 {a:1, c:1} | 1 {c:1}
	```
	
	

### Sliding Windown Solution O(N)

Maintain a window and keep adding elements to the right side of the window.  If unique elements exceeds k, remove elements from the left side until element count equals k.  Finish when the window reach the end of the string.  Keep updating global max result during the loop.

The **key observation** here is that the longest valid substing has exactly k unique elements.  So we only need to conside the substrings that has k unique elements.  If the entire input string has less than k unique elements, the window will be the entire string.

```python
class Solution(object):
    def lengthOfLongestSubstringTwoDistinct(self, s):
        """
        :type s: str
        :rtype: int
        """
        m = {}
        start = end = res = 0
        while end < len(s):
            if s[end] in m:
                m[s[end]] += 1
            else:
                m[s[end]] = 1
                while len(m) > 2:
                    if m[s[start]] < 2:
                        del m[s[start]]
                    else:
                        m[s[start]] -= 1
                    start += 1
            res = max(res, end - start + 1)
            end += 1
        return res
```

---

## Problem 2

[Leetcode #5 Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

> Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

### Brute Force Solution O(N^2)

Notive that a palindrome can be expanded from its center, and there are only 2N-1 ( N + N-1 ) such centers.  Exam every possible center, each center takes most O(N) time, thus overall complexity is O(N^2).

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        if (s.size() <= 1)
            return s;
        int center = 0, j = 0;
        int maxLen = 0, start = 0, end = 0, curLen = 0;
        for (int i = 0; i < 2*s.size() - 1; i++) {
            // 0 # 1 # 2 # 3 # 4 # 5
            // 0 1 2 3 4 5 6 7 8 9 10 center index
            if (i % 2 == 0) {
                center = i / 2;
                j = 1;
                while (center - j >= 0 && center + j < s.size()) {
                    if (s[center-j] == s[center+j]) {
                        curLen = j*2 + 1;
                        if (curLen > maxLen) {
                            maxLen = curLen;
                            start = center - j;
                            end = center + j;
                        }
                        j++;
                    } else {
                        break;   
                    }
                }
            } else {
                center = i / 2;
                j = 1;
                while(center + 1 - j >= 0 && center + j < s.size()) {
                    if (s[center+1-j] == s[center+j]) {
                        curLen = j*2;
                        if (curLen > maxLen) {
                            maxLen = curLen;
                            start = center + 1 - j;
                            end = center + j;
                        }
                        j++;
                    } else {
                        break;
                    }
                }
            }
        }
        // cout << start << " " << end << endl;
        return s.substr(start, end-start+1);
    }
};
```

### Manacher's Algorithm O(N) Time, O(N) Space

[reference](http://articles.leetcode.com/longest-palindromic-substring-part-ii/)

```cpp
// Transform S into T
// S = "abba"
// T = "^#a#b#b#a#$"
// ^ and $ signs are sentinels appended to each end to avoid bounds checking

string preProcess(string s) {
	int n = s.length();
	if (n == 0) return "^$";
	string ret = "^";
	for (int i = 0; i < n; i++) {
		rei += "#" + s.substr(i, 1);
	}
	ret += "#$";
	return ret;
}

string longestPalindrome(string s) {
	string T = preProcess(s);
	int n = T.length();
	int *p = new int[n];
	int C = 0, R = 0;
	for (int i = 1; i < n-1; i++) {
		int i_mirror = 2*C-i; // i` = C - (i-C)
		P[i] = (R > i) ? min(R-i, P[i_mirror]) : 0;
		while (T[i + 1 + P[i]] == T[i - 1 - P[i]])
			P[i]++;
			
		if (i + P[i] > R) {
			C = i;
			R = i + P[i];
		}
	}
	
	int maxLen = 0;
	int centerIndex = 0;
	for (int i = 1; i < n; i++) {
		if (P[i] > maxLen) {
			maxLen = P[i];
			centerIndex = i;
		}
	}
	delete[] P;
	
	return s.substr((centerIndex - 1 - maxLen)/2, maxLen);
}
```