# Quick Sort
Sorts elements one by one by placing a pivot element in its correct place and then repeating for the left and right elements recursively.

When helper returns the updated pivot index, recursively call the pivot helper on the subarray to the left of that index, and the subarray to right of that index. 

**Very helpful Youtube Video:** https://www.youtube.com/watch?v=XE4VP_8Y0BU

## Complexity
1. Time

* Best, Avg: O(nlog(n))
* Worst: O(n<sup>2</sup>) 

> If certain data takes time t and we double the data, we need to make one more breaking old array into left and right and for that one extra array we need to compare n times. Thus O(nlog(n)). Worst case comes when the array is already sorted. The pivot will be at its position and we will make n comparisions to move to the next postion which will be at its postion as well and so on for n times. Thus we get O(n<sup>2</sup>). I way to avoid this is by using ```isSorted(array)``` which checks if an array is sorted.

2. Space

* All: O(log(n))

> When array size is doubled, call stack increases by one (Not satisfied with the answer coz this reasoning fails at merge sort)

### Tips
- The run time of quick sort depends in part on where you select the pivot.
- Ideally the pivot should be chosen so that it's roughly the median value in the data set you're sorting. 
- For simplicty, can choose the pivot to be the first element (this can have consequences later). 

#### Steps
1. Pick a pivot in the array. 
2. Then find the elements smaller than the pivot and elements larger than the pivot. (This is called partitioning which means dividing up the elements). 
3. Now you have: a sub-array of all the numbers less than the pivot. The pivot. A sub-array of all the numbers greater than the pivot. 
4. Call quicksort recursively on the two sub-arrays. 

|| 
1. Pick pivot 
2. Divide/Partition array into two sub-arrays: elements less than pivot, elements greater than pivot
3. Call quicksort recursively on the two sub-arrays 

## Implementation
```javascript
function quickSort(array) {
    if (array.length <= 1) return array;
    let pivot = array[0];
    let pivotPosition = 0;
    for (let i = 1; i < array.length; i++)
        if (array[i] < pivot) {
            pivotPosition++;
            [array[pivotPosition], array[i]] = [array[i], array[pivotPosition]];
        }
    [array[0], array[pivotPosition]] = [array[pivotPosition], array[0]];
    let left = quickSort(array.slice(0, pivotPosition));
    let right = quickSort(array.slice(pivotPosition + 1));
    return [...left, pivot, ...right];
}
```

## Quick Sort with Pivot Helper Implementation
```javascript
function pivot(arr, start=0, end=arr.length+1) {
    // swap function
    function swap(arr, i, j){
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    let pivot = arr[start];
    let swapIdx = start;
    for(var i = start + 1; i < arr.length; i++){
        if(pivot > arr[i]){
            swappIdx++;
            swap(arr, swapIdx, i);
        };
    };
    swap(arr, start, swapIdx);
    return swapIdx;
}

function quickSort(arr, left = 0, right= arr.length - 1){
    if(left < right){
        let pivotIndex = pivot(arr, left, right); //3
        //left
        quickSort(arr, left, pivotIndex-1);
        //right
        quickSort(arr, pivotIndex+1, right);
    };
    
    return arr;
}
```
