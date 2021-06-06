

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>



打算练习一下算法，准备从基本的递归、回溯开始


```


# permutation

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

# combination
solution 1: 回溯

```
"""
leet 78#90
"""
def get_subset(a, pre, ans):
    ans.append(pre)
    for i in range(len(a)):
        if i > 0 and a[i] == a[i-1]:
            continue
        get_subset(a[i+1:], pre + [a[i]], ans)

class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        ans, pre = [], []
        get_subset(sorted(nums), pre, ans)
        return ans
```

solution 2: bit operation
1. n 个不相同元素的集合S，其子集个数为:

$ C_{n}^0 + C_{n}^1 + C_{n}^2 + \dots + C_{n}^n = 2 ^ n $

2. 由此我们可以通过一个n位的数来表示

```
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        ans = []
        for i in range(0, 2**n):
            tmp = []
			skip = False
            for j in range(0, n):
                if i & (1 << j):
                    if j > 0 and nums[j] == nums[j-1] and (i & (1 << (j-1)) == 0):
                        skip = True
                        break
                    tmp.append(nums[j])
			if not skip:
            	ans.append(tmp)
        return ans
```

