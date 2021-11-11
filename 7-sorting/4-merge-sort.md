# Merge Sort
Works on divide and conquer algorithm. General strategy is to keep on splitting the arrays into halves then merging the halves one by one.

## Complexity
1. Time
* All: O(nlog(n))
> Suppose some set of data takes time t. Now if we double the data, we have to make one more splitting step. This is log(n) pattern. But for this additional step we have to make n comparisions as well in the merging step. Thus we get O(nlog(n))

2. Space
* All : O(n)
> More double length of left and right arrays created as n doubles

> Coding Pattern: Avoid while true with breaks inside as it makes the code harder to understand.

### Tips
- In order to implement merge sort, useful to first implement a function responsible for merging two sorted arrays.
- Given two arrays which are sorted, the helper function should create a new array which is also sorted, and consists of all of the elements in the two input arrays.
- The function should run in O(n+m) time and O(n+m) space and should not modify the parameters passed to it. 

### Implementation
```javascript
function mergeSort(arr) {
    if (arr.length <= 1) return arr;
    let mid = Math.floor(arr.length/2)
    let left = mergeSort(arr.slice(0, mid));
    let right = mergeSort(arr.slice(mid));
    return mergeArrays(left, right);
}

function mergeArrays(arr1, arr2) {
    // Given two functions, this function constructs a single sorted array
    let sortedArr = [];
    let i = 0;
    let j = 0;
    while (i < arr1.length && j < arr2.length)
        if (arr2[j] > arr1[i]) {
            sortedArr.push(arr1[i]);
            i++;
        } else {
            sortedArr.push(arr2[j]);
            j++;
        }
    if (pointer1 == array1.length)
        sortedArray = sortedArray.concat(array2.slice(pointer2));
    else
        sortedArray = sortedArray.concat(array1.slice(pointer1));
    return sortedArray
}
```
