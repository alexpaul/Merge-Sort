# Merge-Sort

Merge sort algorithm.

The merge sort algorithm uses a divide and coquer approach to sort an array. 

Below illustrates a series of steps in performing merge sort. 

![sketch of merge sort](https://user-images.githubusercontent.com/1819208/97167268-e5841200-175c-11eb-8e01-a8322e5ffbd6.jpg)

## Merge Sort Implementation 

```swift 
func mergesort(_ arr: [Int]) -> [Int] {
  guard arr.count > 1 else {
    return arr
  }
  let middleIndex = arr.count / 2
  let left = mergesort(Array(arr[..<middleIndex]))
  let right = mergesort(Array(arr[middleIndex...]))
  
  return merge(left: left, right: right)
  
}

func merge(left: [Int], right: [Int])  -> [Int] {
  var result = [Int]()
  
  var leftIndex = 0
  var rightIndex = 0
  
  while leftIndex < left.count &&  rightIndex < right.count {
    let leftElement = left[leftIndex]
    let rightElement = right[rightIndex]
    
    if leftElement < rightElement {
      result.append(leftElement)
      leftIndex += 1
    } else if rightElement < leftElement {
      result.append(rightElement)
      rightIndex += 1
    } else {
      result.append(leftElement)
      leftIndex += 1
      result.append(rightElement)
      rightIndex += 1
    }
  }
  
  if leftIndex < left.count {
    result.append(contentsOf: left[leftIndex...])
  }
  if rightIndex < right.count {
    result.append(contentsOf: right[rightIndex...])
  }
  
  return result
}

mergesort([-3, 5, 0, 5, 8, 4, 1]) // [-3, 0, 1, 4, 5, 5, 8]
mergesort([]) // []
mergesort([1]) // [1]
mergesort([-3, -5]) // [-5, -3]
mergesort([-3, -5, -15]) // [-15, -5, -3]
```
