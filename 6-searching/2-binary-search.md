# Binary Search

Requires sorted array. Unlike linear search which eliminates one number at a time, binary search eliminates half of the array at a time. Works on _divide and conquer._

## Complexity
1. Time
	
	Best: O(1)

	Average: O(log(n))

	Worst: O(log(n))

2. Space: O(1)

### Explanation
Suppose we have 16 length array. Is we perform binary search, we half the array overtime repeatedly. So in the worst case 16=>8=>4=>2=>1. Now if we doubled the size of array we will require one extra step. 32=>16=>8=>4=>2=>1. Thus by if complexity is f(n), by doubling n the steps increase by one. Thus f(n) = log(n). Thus O(log(n))

## Implementation
```javascript
//Using recursion
function binarySearch(array, target, left = 0, right = array.length - 1) {
    // find the middle index
    let middle = Math.floor((left + right) / 2)
    if (array[middle] == target) return middle;
    if (right == left) return -1;
    if (target < array[middle]) return binarySearch(array, target, left, middle - 1);
    
    // target is in the right array
    return binarySearch(array, target, middle + 1, right);
}

//Using While Loop
function binarySearch(target, list){
  let left = 0;
  let right = list.length -1;

  // while no overlap;
  while(left <= right){
    let mid = Math.floor((left + right) / 2);
    if (list[mid] === target) return mid;
    else if (list[mid] < target) {
      // target belongs to the right;
      left = mid + 1;
    } else {
        // target belongs to the left
        right = mid - 1
    }
  }
  return -1;
}
```
