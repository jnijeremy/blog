---
layout: post
title: Leetcode Jump Game

---

###[Jump Game 1](https://leetcode.com/problems/jump-game/):

```
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.
```

###Solution O(n)

Greedy approach, loop through the array, update the farthest reachable index in every iteration.

```cpp
bool canJump(vector<int>& nums) {
    int canReach = 0;
    int len = nums.size();
    for (int i = 0; i < len; i++) {
        if (i <= canReach)
            canReach = max(canReach, nums[i] + i);
    }
    return canReach >= len-1;
}
```


###[Jump Game 2](https://leetcode.com/problems/jump-game-ii/):

```
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = [2,3,1,1,4]

The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)
```

###Solution O(n)

Greedy approach, using a sliding window to loop through the array.

Special Case: 

1. arr.size() == 1 ( starting from the last index );
2. can reach last index from arr[0];

General Case:

loop through index window [start+1, end], find maximum new_end, continue loop [end+1, new_end] until reaching last index or can not move forward.


```cpp
int jump(vector<int>& nums) {
    int len = nums.size();
    if (len == 1)
        return 0;
    
    int start = 0, end = nums[start];
    if (end >= len-1)
        return 1;
        
    int count = 0, new_end;
    
    while (true) {
        count++;
        new_end = end;
        for (int i = start + 1; i <= end; i++) {
            if (nums[i] + i >= len - 1) {
                return count + 1;
            } else if (nums[i] + i > new_end) {
                new_end = nums[i] + i;
            }
        }
        if (new_end == end)
            return -1; // can not reach last index
        else {
            start = end;
            end = new_end;
        }    
    }
    
}
```

###Extension on Jump Game 2: 
jump pass the last index, also need to output the optimal jumps.

###Solution
Same as Jump Game 2, store the greedy choose of new_start in each window iteration.  Return empty vector if can't pass the last index.

```cpp
vector<int> arrayHopper(vector<int> arr) {
    int len = arr.size();
    if (len == 0)
        return {};
    
    int start = 0, end = arr[start];
    
    if (end >= len)
        return {start};
    
    vector<int> result;
    int new_end, new_start = start;
    
    while (true) {
        result.push_back(new_start);
        new_end = end;
        for (int i = start + 1; i <= end; i++) {
            int tmp = arr[i] + i;
            if (tmp >= len) {
                result.psuh_back(i);
                return result;
            } else if (tmp > new_end) {
                new_end = tmp;
                new_start = i;
            }
        }
        if (new_end == end)
            return {};
        else {
            start = end;
            end = new_end;
        }
    }
}       
```