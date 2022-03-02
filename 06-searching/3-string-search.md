# String Search
Given a string and a target string, find if the target string is a substring of the main string. Return the number of times the target string mathes with the substring

## Naive Approach
```javascript
// Loop over both the strings and compare charecter by charecter
function stringSearch(string, target) {
    let count = 0
    for(let i = 0; i < string.length; i++) {
        for(let j = 0; j < target.length; j++) {
            if(string[i + j] !== target[j]) break;
            
            if(j === target.length-1) count++;
        }
    }
    return count;
}
```

### Complexity
1. Time: O(n<sup>2</sup>)
2. Space: O(1)
