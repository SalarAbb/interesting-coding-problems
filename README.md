# interesting-coding-problems
Here I list interesting coding problems I have seen over the internet

## 1. Continueous subarray with maximum sum, aka Kardane's algorithm ([link](https://practice.geeksforgeeks.org/problems/kadanes-algorithm/0))
My solution:
```
import sys
def max_sum(arr):
    if max(arr) <= 0:
        return max(arr)
        
    max_sum = 0
    max_end_at_here = 0
    for i in range(len(arr)):
        max_end_at_here = max_end_at_here + arr[i]
        if max_end_at_here < 0:
            max_end_at_here = 0
        
        max_sum = max(max_sum, max_end_at_here)
    
    return max_sum        
    
    
i = 0 
cases = {}
for line in sys.stdin:
    line = line.strip()
    if i == 0:
        num_test_cases = int(line)
    else:
        if i % 2 == 0:
            line = line.split(' ')
            cases[int(i/2 - 1)] = [int(j) for j in line]
        
    i += 1
#print(cases)
# now cases is the dictionary of all test cases
for i in range(len(cases)):
    arr_this = cases[i]
    print(max_sum(arr_this))
```    
## 2. Minimum window substring ([link](https://leetcode.com/problems/minimum-window-substring/submissions/))

My solution (another interesting solutions is using 2 pointers to expand from right and contract from left):
```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        # create a dictionary for recent t
        t_list = list(t)
        t_dict = {i:-1 for i in t}        
        
        n = len(s)
        min_sub_length = 2 * n
        min_win = ""
        
        for i, curr_s in enumerate(list(s)):
            if curr_s in t_dict:
                t_dict[curr_s] = i
            vals = list(t_dict.values())
            if -1 not in vals:
                new_win_min = min(vals)
                new_win_max = max(vals)
                new_win_length = new_win_max - new_win_min + 1
                if new_win_length < min_sub_length:
                    min_win = s[new_win_min:new_win_max + 1]
                    min_sub_length = new_win_length
                    
        print(t_dict)
        return min_win
```
