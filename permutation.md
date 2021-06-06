


打算练习一下算法，准备从基本的递归、回溯开始


```

"""
leet46/leet47: permutation (with duplicates)
"""

def perm(a, pre, ans):
    if len(a) == 0:
        ans.append(pre)
    for i in range(len(a)):
        if i > 0 and a[i] == a[i-1]:
            continue
        perm(a[:i] + a[i+1:], pre + [a[i]], ans)

class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        ans, pre = [], []
        perm(sorted(nums), pre, ans)
        return ans
```
