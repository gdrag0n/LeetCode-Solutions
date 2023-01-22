# Approach 1

I do not plan to use three for loops.
The only way that can be implemented in my opinion would be to find the third value in nums instead, since we already know what sets we are looking for and what condition must be satisfied for the same.

*Problem outline:
a=nums[i]
b=nums[j]
c=nums[k]
c=-(a+b) for a+b+c=0 to satisfy
if c is in nums, and its index is not same as a and b, its value is acceptable*

```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:

        l=[]
        n=len(nums)
        for i in range(n):
            for j in range(i+1,n):
                a=nums[i]
                b=nums[j]
                c=-(a+b)
                if c in nums:
                    p=nums.index(c)
                    if p!=i and p!=j:
                        l.append(sorted([a,b,c]))
                        #l=[[-1,0,1],[-1,0,1],[-1,-1,2],[-1,0,1],[-1,0,1],[-1,0,1],[-1,-1,2]]
        
        for i in l:
            if l.count(i)>1:
                l.remove(i)
        
        return l
```
nums: [-1,0,1,2,-1,-4]
Expected Output: [[-1,-1,2],[-1,0,1]]
Output: [[-1,0,1],[-1,0,1],[-1,0,1],[-1,-1,2]]

Since List is not hashable, l=list(dict.fromkeys(l)) does not remove duplicates.
I decide to remove duplicates by, well. deleting duplicates

# Approach 02
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:

        l=[]
        n=len(nums)
        for i in range(n):
            for j in range(i+1,n):
                a=nums[i]
                b=nums[j]
                c=-(a+b)
                if c in nums:
                    p=nums.index(c)
                    if p!=i and p!=j:
                        l.append(sorted([a,b,c]))
        
        for i in l:
            for j in range(l.count(i)-1):
                l.remove(i)
        
        return sorted(l)
```

nums = [-1,0,1,2,-1,-4,-2,-3,3,0,4]
146 / 312 testcases passed
Output:
[[-1,-1,2],[-1,-1,2],[-3,1,2],[-1,0,1],[-4,1,3],[-2,-1,3],[-2,0,2],[-3,-1,4],[-3,0,3],[-4,0,4]]
Expected:
[[-4,0,4],[-4,1,3],[-3,-1,4],[-3,0,3],[-3,1,2],[-2,-1,3],[-2,0,2],[-1,-1,2],[-1,0,1]]




To understand the issue more, I decided to implement the problem till before duplicates are removed.
```
l=
[[-4,0,4],[-4,0,4],[-4,0,4],[-4,0,4],[-4,0,4],[-4,1,3],[-4,1,3],[-4,1,3],
[-3,-1,4],[-3,-1,4],[-3,-1,4],[-3,-1,4],[-3,-1,4],[-3,0,3],[-3,0,3],[-3,0,3],[-3,0,3],[-3,0,3],[-3,1,2],[-3,1,2],[-3,1,2],
[-2,-1,3],[-2,-1,3],[-2,-1,3],[-2,-1,3],[-2,-1,3],[-2,0,2],[-2,0,2],[-2,0,2],[-2,0,2],[-2,0,2],
[-1,-1,2],[-1,-1,2],[-1,0,1],[-1,0,1],[-1,0,1],[-1,0,1],[-1,0,1],[-1,0,1],[-1,0,1],[-1,0,1]]
```
[-1,-1,2] gets repeated
Understanding the code:

i=[-1,-1,2]
l.count(i)=2
j in range(1):
    l.remove(i)
    
i should be removed once for j=0
but it isnt ;;