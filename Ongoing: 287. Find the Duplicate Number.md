# Approach 01
```
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:

        for i in nums:
            if nums.count(i)>1:
                return i
```

Time Exceed

# Approach 02
```
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:

        n=len(nums)
        return sum(nums)-sum(list(range(n)))
        #or return sum(nums)- (n*(n+1)/2)

```

# Approach 03
```

```
