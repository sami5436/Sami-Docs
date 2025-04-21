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

4 -  Is Subsequence
Input: s = "abc", t = "ahbgdc"
Output: true

- do the characters in s appear in t? do the characters in s appear in t in the original order they appear in s?
  ```
  class Solution:
      def isSubsequence(self, s: str, t: str) -> bool:
          sI, tI = 0, 0
          while (sI < len(s) and tI < len(t)):
              if(s[sI] == t[tI]):
                  sI += 1
              tI += 1
          
          return sI == len(s)
          
  ```
  **Thought Process**: used 2 pointers to keep track of character s and character t. while the pointers were in bound, i check to see if current characters are equal. if they are, we can move both indicies to next pos. if not, we only move t since we havent found the s index yet. if while loop is exited, we check s index to see if s has been iterated thru entirely.

  
5 -  Best Time to Buy and Sell Stock

Input: prices = [7,1,5,3,6,4]
Output: 5

- what is the profit (left index being the min and and right index being the max after the min occurrence) 
  ```
  class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        l, r, maxP = 0, 1, 0

        while(r < len(prices)):
            if prices[r] > prices[l]:
                profit = prices[r] - prices[l]
                maxP = max(maxP, profit)
            else:
                l = r
            r += 1
        
        return maxP
          
  ```
  **Thought Process**: used left and right, right is always ahead of left. we are always going to increment right by one at every iteration, if we hit a place where our right is less then our left value, this is saying hey we found a new low, we need to readjust our left. if not (price at right is greater than price at left, what its supposed to be), then we just do a normal profit calc and we can just make sure to replace the maxP var if it is greater.

6 -  Longest Common Prefix

Input: strs = ["flower","flow","flight"]
Output: "fl"

- prefix 
  ```
  class Solution:
      def longestCommonPrefix(self, strs: List[str]) -> str:
          if not strs:
              return ""
          
          for i in range(len(strs[0])):
              char = strs[0][i]
              for word in strs[1:]:
                  if i >= len(word) or word[i] != strs[0][i]:
                      return strs[0][:i]
          return strs[0]
          
  ```
  **Thought Process**: right so the longest possible prefix is the first string completely so we iterate thru the entire word char by char and use that to compare char by char to the other words chars at that specific index. we are not rlly adding chars to any variable, we are just straight up moving on with the first word's index if we keep hitting matches. if at the current word we are comparing has lesser length than the index var, we just return wherever the slice of whereever we stopped or if the current value of the word we are checking compared to first word's char at that specific index, we also return the slice of where ever we stopped
  
  
  

