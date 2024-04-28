# CyberCode
Coding challenges in Transformers/Cybertron setting. Mostly from leetcode.

### 55. Jump Game
You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

Example 1:

Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
Example 2:

Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
 
Constraints:
1 <= nums.length <= $10^4$
0 <= nums[i] <= $10^5$

```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        # index=0
        # for i in range(len(nums)):
        #     if i+nums[i]>=index:
        #         index=i+nums[i]
        #     if i >= index:
        #         break
        # return index>=len(nums)-1
        """
        greedy algorithm
        KEEP: max index possible
        BREAK: cannot reach the index
        max index: just add up the index and the according number in the list
        cannot reach: if current index cannot be reached by current max index 
        """
        cubes=0
        for cube in nums:
            if cubes<0:
                return False
            elif cube>cubes:
                cubes=cube
            cubes-=1
        return True
        """
        energon replacement strategy
        set energon cubes to 0
        traverse the whole engergon supplies:
        replace with new supply if more cubes than current
        each step cost one cube
        if cubes<0, stasis return false
        if successfully traversed list, return True
        """
```

### 45. Jump Game II
You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].

Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:

0 <= j <= nums[i] and
i + j < n
Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].

Example 1:

Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
Example 2:

Input: nums = [2,3,0,1,4]
Output: 2
 

Constraints:

1 <= nums.length <= 10^4
0 <= nums[i] <= 1000
It's guaranteed that you can reach nums[n - 1].
```
class Solution:
    def jump(self, nums: List[int]) -> int:
        reach, step, last = 0,0,0
        for i in range(len(nums)-1):
            reach=max(reach,i+nums[i])
            if reach>=len(nums)-1:
                step+=1
                break
            if i == last:
                last=reach
                step+=1
        return step
        """
        Q: how to reach the last energon mine with least steps
        A: find the farthest reach of mines within each mines reachable range
        (Because it's bound that the last one shall be reached)
        Keep: 
        reach: farthest reach of mines within each energon mine's range,
        step: number of steps
        last: end point of each energon mine's reachable range
        Update:
        reach: max(i+nums[i])
        step: if reach the furthest mine of each step, +1
        or if reach the last mine, +1 and BREAK
        """
```
