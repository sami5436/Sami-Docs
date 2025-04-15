# Leetcode

1 - Find Closest Number to Zero

- Given an integer array of nums, return the value that is closest to 0. If 2 values are the same distance from 0, return the larger one (positive)
  - [2, -1, 1] -> 1
  ```
  class Solution:
    def findClosestNumber(self, nums: List[int]) -> int:
        closest = nums[0]
        for num in nums:
            if abs(num) < closest:
                closest = num
            
        if(closest < 0 and abs(closest) in nums):
            return abs(closest)
        return closest
  ```
  **Thought Process**: basically, iterate thru the array and find the closest number. if the positive version of the closest number exists within the array, return that instead of the closest number.

  

