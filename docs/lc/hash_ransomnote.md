Input: ransomNote = "aa", magazine = "aab"
Output: true

so the idea is we need to check if ransomnote's characters are less than or equal to the count of that respective character.

we can use hashmaps to solve this for us. we use that counter method thingy to convert all the chars into a dict real easy


```
def canConstruct(self, ransomNote: str, magazine: str) -> bool:
    ransom_char_dict, magazine_char_dict = Counter(ransomNote), Counter(magazine)
    for char, count in ransom_char_dict:
        if count > magazine_char_dict[char]: Return False # hey if we have more characters in ransom, we obv cant reproduce that using the magazine's characters.
    return True
```