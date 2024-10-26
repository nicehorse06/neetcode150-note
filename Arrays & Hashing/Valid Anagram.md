# [Valid Anagram](https://neetcode.io/problems/is-anagram)

## 解法一
* 先建立一個dict
* for第一個string，把每個值出現的次數存進去dict
* 再for第二個string扣掉出現的次數
* 只要dict每個值為0的場景，才是合格Valid Anagram

## 解法二
* 改用長度為26的list來存，空間複雜度比dict好
  * 26為小寫字母數目
* 依據第一個string長度做for，每次拿第一個字母位置的值+1，第二個字母的值-1
  * 如果是一樣的string，最後會抵銷成0
* 最後再檢查list是否都為0就是答案


``` python
# 解法一
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # 如果字串長度不一樣，直接返回 False
        if len(s) != len(t):
            return False
        
        # 記錄 s 中每個字母的出現次數
        record = {}

        for c in s:
            record[c] = record.get(c, 0) + 1
        
        # 檢查 t 中每個字母是否能對應到 record
        for c in t:
            if c not in record:  # t 中出現了 s 中不存在的字母
                return False
            record[c] -= 1
            if record[c] < 0:  # 如果某個字母出現次數超過 s 中的次數
                return False

        # 檢查所有字母的次數是否為 0
        return all(val == 0 for val in record.values())
```

``` python
# 解法二
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # 首先檢查兩個字串的長度，如果不同直接返回 False
        if len(s) != len(t):
            return False

        # 建立一個長度為 26 的陣列，用來記錄 a-z 的字母出現次數
        count = [0] * 26
        
        # 遍歷字串 s 和 t，計算每個字母在 s 和 t 中的出現次數差異
        for i in range(len(s)):
            # 將 s 中的字母對應的陣列位置加 1
            count[ord(s[i]) - ord('a')] += 1
            # 將 t 中的字母對應的陣列位置減 1
            count[ord(t[i]) - ord('a')] -= 1

        # 最後檢查陣列中的每個值是否都為 0
        # 若有不為 0 的，代表 s 和 t 中字母的出現次數不相等，返回 False
        for val in count:
            if val != 0:
                return False
        
        # 若所有值都是 0，代表 s 和 t 是字母異位詞，返回 True
        return True

```