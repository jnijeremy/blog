---
layout: post
title: Leetcode 39 Combination Sum
---

[Problem](https://leetcode.com/problems/combination-sum/):

```
Given a set of candidate numbers (C) and a target number (T), 
find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

For example, given candidate set 2,3,6,7 and target 7, 
A solution set is: 
[7] 
[2, 2, 3] 
```

Navie solution: use dfs to traverse all possible combinations of candidates, the time complexity is exponential.  Solution will have duplicates.

Optimization: sort candidates at the beginning, traversal candidates in order by passsing the index of current node. (resursion only consider candidates at and after current index i).

```cpp
/*
Leetcode 39 Combination Sum
https://leetcode.com/problems/combination-sum/
Author: Jeremy Ni
*/
#include <bits/stdc++.h>
using namespace std;

void dfs(vector<int>& candidates, int target, int i, vector<int>& path, vector<vector<int>>& result) {
  if (target == 0) {
    result.push_back(path);
    return;
  }
  for (int j = i; j < int(candidates.size()); j++) {
    int x = candidates[j];
    if (target >= x) {
      path.push_back(x);
      dfs(candidates, target-x, j, path, result);
      path.pop_back();
    }
  }
}

vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
  vector<int> path;
  vector<vector<int>> result;
  sort(candidates.begin(), candidates.end());
  dfs(candidates, target, 0, path, result);
  return result;
}

struct TestCase {
  vector<int> t;
  int target;
  TestCase(vector<int> x, int y) : t(x), target(y) {}
};

int main() {
  vector<TestCase> T;
  
  vector<int> t1 = {2,3,6,7};
  TestCase T1 = TestCase(t1, 7); 
  T.push_back(T1);

  vector<int> t2 = {};
  TestCase T2 = TestCase(t2, 7); 
  T.push_back(T2);
  
  vector<int> t3 = {2,3,6,7};
  TestCase T3 = TestCase(t3, 1); 
  T.push_back(T3);

  vector<int> t4 = {1};
  TestCase T4 = TestCase(t4, 7); 
  T.push_back(T4);
  
  vector<vector<int>>result;
  
  for (auto t:T) {
    cout << "test case:" << endl;
    cout << "{ ";
    for (auto i: t.t) {
      cout << i << " ";
    }
    cout << "}, target = " << t.target << endl;
    
    result = combinationSum(t.t, t.target);
    cout << "result:" << endl;
    for (auto x:result) {
      for (auto y:x) {
        cout << y << " ";
      }
      cout << endl;
    }
  }
  return 0;
}
```