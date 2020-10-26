# Merge-Sort

Merge sort algorithm.

The merge sort algorithm uses a divide and coquer approach to sort an array. 

The runtime of merge sort is `O(n log n)` .

Below illustrates a series of steps in performing merge sort. 

1. Find the middle index of the array.
2. Divide the array in a left and right side using the middle index. `O(log n)` runtime. 
3. The base case for stopping the divide and conquer process is when we have 1 element left. 
4. Merge back the divided arrays while sorting the elements. `O(n)` runtime. 

![sketch of merge sort](https://user-images.githubusercontent.com/1819208/97173227-98a53900-1766-11eb-9d01-cb9842ae88a6.jpg)


## Merge Sort Implementation 

```swift 
// merge sort

// 2 parts

// divide and conquer
// mergesort using recursion
// 2 parts of a recursive function
// 1. base case
// 2. recursive call
func mergesort(_ arr: [Int]) -> [Int] { // O(nlogn)
  // 3 - base case
  guard arr.count > 1 else {
    return arr
  }
  // 1 - middle index
  let middleIndex = arr.count / 2
  
  // 2 - use divide and conquer to split array in halves => runtime O(log n)
  let leftArr = mergesort(Array(arr[..<middleIndex])) // ..< middleIndex - does not include middleIndex
  let rightArr = mergesort(Array(arr[middleIndex...]))
  
  // 4 - merge elements while sorting
  return merge(leftArr: leftArr, rightArr: rightArr)
}

// merge sorted arrays
func merge(leftArr: [Int], rightArr: [Int]) -> [Int] { // O(n)
  var results = [Int]()
  var leftIndex = 0
  var rightIndex = 0
  
  // 4a
  while leftIndex < leftArr.count && rightIndex < rightArr.count {
    let leftElement = leftArr[leftIndex]
    let rightElement = rightArr[rightIndex]
    
    if leftElement < rightElement {
      results.append(leftElement)
      leftIndex += 1
    } else if rightElement < leftElement {
      results.append(rightElement)
      rightIndex += 1
    } else { // there're equal - add both elements to the results array
      results.append(leftElement)
      leftIndex += 1
      results.append(rightElement)
      rightIndex += 1
    }
  }
  
  // 4b - add remaining elements if any
  if leftIndex < leftArr.count { // values we have not seen
    results.append(contentsOf: leftArr[leftIndex...])
  }
  
  if rightIndex < rightArr.count {
    results.append(contentsOf: rightArr[rightIndex...])
  }
  
  return results
}

mergesort([-3, 5, 0, 5, 8, 4, 1]) // [-3, 0, 1, 4, 5, 5, 8]
mergesort([]) // []
mergesort([1]) // [1]
mergesort([-3, -5]) // [-5, -3]
mergesort([-3, -5, -15]) // [-15, -5, -3]
```
