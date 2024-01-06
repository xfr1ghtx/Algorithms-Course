# Stacks
# [LeetCode](https://leetcode.com/list/pl2tmlz3)

## [Lecture](https://disk.yandex.ru/i/6jXOX07CMBVplQ)

### Task:

**_Valid Parentheses_**
<details>
<summary>Code</summary>

```Swift
class Solution {
    func isValid(_ s: String) -> Bool {
        var stack = [Character]()
        
        for char in s {
            if char == "(" || char == "{" || char == "[" {
                stack.append(char)
            } else {
                guard !stack.isEmpty else { return false }
                let lastChar = stack.removeLast()
                if char == ")" && lastChar == "(" {
                    continue
                } else if char == "}" && lastChar == "{" {
                    continue
                } else if char == "]" && lastChar == "[" {
                    continue
                } else {
                    return false
                }
            }
        }
        
        return stack.isEmpty
    }
}
```
or
```Swift
class Solution {
    func isValid(_ s: String) -> Bool {
        
        guard s.count % 2 == 0 else { return false }
        
        var stack: [Character] = []
        
        for ch in s {
            switch ch {
            case "(": stack.append(")")
            case "[": stack.append("]")
            case "{": stack.append("}")
            default:
                if stack.isEmpty || stack.removeLast() != ch {
                    return false
                }
            }
        }
        
        return stack.isEmpty
    }
}
```

</details>

**_Min Stack_**
<details>
<summary>Code</summary>

```Swift
class MinStack {

    private var stack = Array<Int>()
    private var minValueStack = Array<Int>()

    init() {}
    
    func push(_ val: Int) {
        stack.append(val)
        if let lastMin = minValueStack.last {
            if lastMin < val {
                minValueStack.append(lastMin)
            } else {
                minValueStack.append(val)
            }
        } else {
            minValueStack.append(val)
        }
    }
    
    func pop() {
        _ = stack.popLast()
        _ = minValueStack.popLast()
    }
    
    func top() -> Int {
        guard let top = stack.last else { return -1 }
        return top
    }
    
    func getMin() -> Int {
        guard let min = minValueStack.last else { return -1 }
        return min
    }
}
```
or 
```Swift
class MinStack {

    private var array: [(element: Int, minValue: Int)] = []
    
    func push(_ val: Int) {
        if let last = array.last {
            array.append((val, min(val, last.minValue)))
        } else {
            array.append((val, val))
        }
    }
    
    func pop() {
        array.removeLast()
    }
    
    func top() -> Int {
        array.last?.element ?? 0
    }
    
    func getMin() -> Int {
        array.last?.minValue ?? 0
    }

}
```

</details>

**_Baseball Games_**
<details>
<summary>Code</summary>

```Swift
class Solution {
    func calPoints(_ operations: [String]) -> Int {
        var stack = Array<Int>()
        
        for operation in operations {
            if let number = operation.isNumber() {
                stack.append(number)
            } else if operation == "C" {
                _ = stack.popLast()
            } else if operation == "+" {
                guard let first = stack.popLast(), let second = stack.popLast() else { return 0 }
                stack.append(second)
                stack.append(first)
                stack.append(second + first)
            } else if operation == "D" {
                guard let last = stack.last else { return 0 }
                stack.append(last * 2)
            }
        }
        
        if stack.isEmpty { return 0 }
        
        var sum = 0
        stack.forEach {
            sum += $0
        }
        
        return sum
    }
}

extension String {
    func isNumber() -> Int? {
        guard let number = Int(self) else { return nil }
        return number
    }
}
```
or
```Swift
class Solution {
    func calPoints(_ operations: [String]) -> Int {
        var record = [Int]()
        for op in operations {
            switch op {
            case "D":
                let last = record[record.count-1]
                record.append(last*2)
            case "C":
                record = Array(record[0..<record.count-1]) // record.dropLast()
            case "+":
                let last1 = record[record.count-1]
                let last2 = record[record.count-2]
                record.append(last1 + last2)
            default:
                record.append(Int(op) ?? 0)
            }
        }
        return record.reduce(0) { partialResult, s in
            partialResult + s
        }
    }
}
```
or
```Swift
class Solution {
    func calPoints(_ operations: [String]) -> Int {
        var result: [Int] = []
        for s in operations {
            switch s {
            case "D":
                result += [result.last! * 2]
            case "C":
                result = result.dropLast()
            case "+":
                result += [result[result.count - 2] + result.last!]
            default:
                result += [Int(s)!]
            }
        }
        return result.reduce(0, +)
    }
}
```

</details>