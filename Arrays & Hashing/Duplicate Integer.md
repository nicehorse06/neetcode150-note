# [Duplicate Integer](https://neetcode.io/problems/duplicate-integer)

用set去記錄每個值，for有重複到就回傳

``` python
class Solution:
    def hasDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        # set是用hash去實做的，所以num in nums的時間複雜度為常數
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return Falsec
```