# merge intervals


Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]

```
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        res = []
        intervals.sort(key = lambda x : x[0])
        res.append(intervals[0])
        # when it comes to this problem we need to make sure we always sort
        # we are going to traverse now using the start, end of every interval
        # we will store the lastEnd (first iteration, itll be the first interval)
        # we check hey is our current intervals start less than or equal to our lastEnd
        # if it is (ex - cur: (1,6). last: (0, 5)), so you take the max 
        # and u store it as ur "new" lastEnd (in this case its the same)
        # if not, lets say we have (0, 3) (4, 7). obv our last end is smaller, so we hit the
        # else and just add the current interval 

        for start, end in intervals[1:]:
            lastEnd = res[-1][1]

            if start <= lastEnd:
                res[-1][1] = max(lastEnd, end)
            else:
                res.append([start, end])
        return res
```

**thought process**: the idea is you add the first interval, since its sorted it is for sure in the correct place. you then iterate thru the rest of the intervals. if an interval's start point is less than the interval within the result array, this indicates that we have an overlap of some sort. we need to possibly readjust our interval within our result array (the one we are referncing called lastEnd). we need to take the max of lastEnd and current interval's end and update the end of that referencd interval within our result array
if not, we just add that interval to the result array (no overlap)
