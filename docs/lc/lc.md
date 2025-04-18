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

  
2 - Merge Strings Alternately

- You are given 2 strings. Add letter by letter to result starting on the left word and alternating to the right. If you fully iterate a string and still have some characters left in the other string, add it to the end of result. 
  - Input: word1 = "abc", word2 = "pqr"
  - Output: "apbqcr"
  ```
  class Solution:
      def mergeAlternately(self, word1: str, word2: str) -> str:
          left, right = 0, 0
          res = ""
          while left < len(word1) and right < len(word2):
              res += word1[left]
              res += word2[right]
              left += 1
              right += 1
          
          if left < len(word1):
              res += word1[left:]
          
          if right < len(word2):
              res += word2[right:]
        
  ```
  **Thought Process**: have 2 vars to store the indices of the left and the right. add the left words current index to result, then right words current index to result. as soon as youre done iterating thru either left or right word, end while loop. this indicates that there may be more characters in one of the words, append the rest of the word to it.

3 -  Roman to Integer
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

- Roman to integer. 
  ```
  class Solution:
      def romanToInt(self, s: str) -> int:
          d = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
          res = 0
  
          for a, b in zip(s, s[1: ]):
              if d[a] < d[b]:
                  res -= d[a]
              else:
                  res += d[a]
  
          return res + d[s[-1]]
        
  ```
  **Thought Process**: created a dictionary and store all roman to integer vals. a iterating thru s while b is iterating thru s[1:] at the same with the zip function. at every iteratation a is compared to b, and if a is less than b subtract, else add.
