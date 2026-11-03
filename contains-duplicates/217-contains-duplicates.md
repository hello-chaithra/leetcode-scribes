## LeetCode number: 217 | Contains Duplicates 
- *Data structure:* hash set (unordered_set<int>)
- *Algorithm:* single pass with membership check

## Concept and complexity
Walk the array. If the current value is already in the set, return true, otherwise insert it.
- **Time:** O(n)
- **Space:** O(n)
  
## Solution

```cpp
bool containsDuplicate(vector<int>& nums) {
    unordered_set<int> seen;
    for (int x : nums) {
        if (!seen.insert(x).second) return true; // insert fails => already present
    }
    return false;
}
```

insert returns a pair<iterator,bool>, and the bool is false if the element already existed. That saves a separate lookup.
