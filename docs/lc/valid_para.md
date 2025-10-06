```
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        pairs = {')': '(', ']': '[', '}': '{'}
        
        for ch in s:
            if ch in pairs.values():
                stack.append(ch)
            elif ch in pairs:
                if not stack or stack[-1] != pairs[ch]:
                    return False
                stack.pop()
            else:
                pass
        
        return not stack

```

rlly easy. idea is add all opens brackets to stack

if you hit a closed bracket, peek the stack. if the peek isnt the respective bracket, return false. pop right after and conitnue 
