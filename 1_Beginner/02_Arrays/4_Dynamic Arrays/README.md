# Dynamic Arrays
# [LeetCode](https://leetcode.com/list/pl2txr5g)

## [Lecture](https://disk.yandex.ru/i/NRsdxejhtJRIUQ)

### Task:

**_Concatenation of Array_**
<details>
<summary>Code</summary>

```Swift
class Solution {
    func getConcatenation(_ nums: [Int]) -> [Int] {
        var result = Array<Int>(repeating: 0, count: nums.count * 2)
        
        for (index, element) in nums.enumerated() {
            result[index] = element
            result[index + nums.count] = element
        }
        
        return result
    }
}
```
or
```Swift
class Solution {
    func getConcatenation(_ nums: [Int]) -> [Int] {
        return nums + nums
    }
}
```
or
```Swift
class Solution {
    func getConcatenation(_ nums: [Int]) -> [Int] {
        var result = nums

        for i in 0..<nums.count{
            result.append(nums[i])
        }

        return result
    }
}
```
</details>