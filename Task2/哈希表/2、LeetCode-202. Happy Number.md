## 202. Happy Number
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.
## 代码
```p
class Solution:
    def isHappy(self, n: int) -> bool:
        d = {}
        while True:
            #得到每个数字，也可以循环除10
            listn = list(map(int,str(n)))
            sum = 0
            for i in listn:
                sum += i**2
            if sum == 1:
                return True
            if sum in d:
                return False
            n = sum
            d[sum] = sum
```
### 总结
求完每个数字的平方之后，如果这个数字为1那么就是HAPPY NUMBER ，如果开始循环的话，那么就不是。将每次得到的结果放到字典中，判断是否重复出现。最后的字典也可以是集合或者列表。
