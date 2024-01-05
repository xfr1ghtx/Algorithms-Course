# Static Arrays
# [LeetCode](https://leetcode.com/list/pl2ukats)

## [Lecture](https://disk.yandex.ru/i/3iYvyJ31tR7pbQ)

### Tasks:

**_Remove Duplicates from Sorted Array_**
<details>
<summary>Code</summary>

```Swift
class Solution {
    func removeDuplicates(_ nums: inout [Int]) -> Int {
        var lastElement = nums[0]
        var lastElementIndex = 0
        
        for index in 1..<nums.count {
            if lastElement != nums[index] {
                lastElement = nums[index]
                lastElementIndex += 1
            }
            nums[lastElementIndex] = nums[index]
        }
        
        return lastElementIndex + 1
    }
}
```

</details>

**_Remove Element_**
<details>
<summary>Code</summary>

```Swift
class Solution {
    func removeElement(_ nums: inout [Int], _ val: Int) -> Int {
        var counter = 0
        
        for number in nums {
            if number != val {
                nums[counter] = number
                counter += 1
            }
        }

        return counter
    }
}
```

</details>

**_Shuffle the Array_**
<details>
<summary>Code</summary>

```Swift
class Solution {
    func shuffle(_ nums: [Int], _ n: Int) -> [Int] {
        var indexX = 0
        var indexY = n
        var res = nums
        
        for index in 0..<nums.count {
            if index % 2 == 0 {
                res[index] = nums[indexX]
                indexX+=1
            } else {
                res[index] = nums[indexY]
                indexY+=1
            }
        }
        return res
    }
}
```

</details>