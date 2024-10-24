# [Two Sum](https://neetcode.io/problems/two-integer-sum)

  * 用一個for把nums裡面取出num_1並藉由target推算num2，把這個值和index關係存到dict，如果nums存在num_2就知道答案
* 時間複雜度n

``` python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        this_dict = {}

        for i in range(len(nums)):
            if nums[i] in this_dict:
                return [this_dict[nums[i]], i]
            else:
                # target - nums[i]為nums[i]預期對應的答案，把這個數跟index存到dict中，下次對應數出現時就回傳
                this_dict[target - nums[i]] = i
```